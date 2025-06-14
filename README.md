"use client"

import type React from "react"
import { useState, useEffect } from "react"
import { Button } from "@/components/ui/button"
import { Card, CardContent } from "@/components/ui/card"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Dialog, DialogContent, DialogHeader, DialogTitle } from "@/components/ui/dialog"
import { Alert, AlertDescription } from "@/components/ui/alert"
import { useToast } from "@/hooks/use-toast"
import {
  MoreVertical,
  Trash2,
  ExternalLink,
  PartyPopper,
  MessageCircle,
  Users,
  ChevronLeft,
  ChevronRight,
  Loader2,
  Database,
} from "lucide-react"
import { DropdownMenu, DropdownMenuContent, DropdownMenuItem, DropdownMenuTrigger } from "@/components/ui/dropdown-menu"
import { supabase, type Chat } from "@/lib/supabase"

const CHATS_PER_PAGE = 9

export default function QuinceaneraMTY() {
  const [activeTab, setActiveTab] = useState<"upload" | "all" | "my">("upload")
  const [chats, setChats] = useState<Chat[]>([])
  const [myChats, setMyChats] = useState<Chat[]>([])
  const [title, setTitle] = useState("")
  const [link, setLink] = useState("")
  const [error, setError] = useState("")
  const [loading, setLoading] = useState(false)
  const [showSuccess, setShowSuccess] = useState(false)
  const [selectedChat, setSelectedChat] = useState<Chat | null>(null)
  const [userId] = useState(() => {
    if (typeof window !== "undefined") {
      let id = localStorage.getItem("quinceanera-user-id")
      if (!id) {
        id = "user_" + Math.random().toString(36).substr(2, 9)
        localStorage.setItem("quinceanera-user-id", id)
      }
      return id
    }
    return "user_" + Math.random().toString(36).substr(2, 9)
  })
  const [allChatsPage, setAllChatsPage] = useState(1)
  const [myChatsPage, setMyChatsPage] = useState(1)
  const { toast } = useToast()

  useEffect(() => {
    loadAllChats()
    loadMyChats()

    // Configurar suscripción en tiempo real
    const subscription = supabase
      .channel("quinceanera_chats")
      .on("postgres_changes", { event: "INSERT", schema: "public", table: "quinceanera_chats" }, (payload) => {
        const newChat = payload.new as Chat
        setChats((prev) => [newChat, ...prev])

        if (newChat.user_id === userId) {
          setMyChats((prev) => [newChat, ...prev])
        }

        if (newChat.user_id !== userId) {
          toast({
            title: "¡Nuevo chat!",
            description: `Se agregó: ${newChat.title}`,
          })
        }
      })
      .on("postgres_changes", { event: "DELETE", schema: "public", table: "quinceanera_chats" }, (payload) => {
        const deletedId = payload.old.id
        setChats((prev) => prev.filter((chat) => chat.id !== deletedId))
        setMyChats((prev) => prev.filter((chat) => chat.id !== deletedId))
      })
      .subscribe()

    return () => {
      subscription.unsubscribe()
    }
  }, [userId, toast])

  const loadAllChats = async () => {
    try {
      const { data, error } = await supabase
        .from("quinceanera_chats")
        .select("*")
        .order("created_at", { ascending: false })

      if (error) throw error
      setChats(data || [])
    } catch (error) {
      console.error("Error loading chats:", error)
    }
  }

  const loadMyChats = async () => {
    try {
      const { data, error } = await supabase
        .from("quinceanera_chats")
        .select("*")
        .eq("user_id", userId)
        .order("created_at", { ascending: false })

      if (error) throw error
      setMyChats(data || [])
    } catch (error) {
      console.error("Error loading my chats:", error)
    }
  }

  const isValidWhatsAppLink = (url: string) => {
    const whatsappRegex = /^https:\/\/chat\.whatsapp\.com\/[A-Za-z0-9]+$/
    return whatsappRegex.test(url)
  }

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setError("")
    setLoading(true)

    if (!title.trim() || !link.trim()) {
      setError("Por favor completa todos los campos")
      setLoading(false)
      return
    }

    if (!isValidWhatsAppLink(link)) {
      setError("Solo se aceptan links de WhatsApp válidos (https://chat.whatsapp.com/...)")
      setLoading(false)
      return
    }

    try {
      const { error } = await supabase.from("quinceanera_chats").insert([
        {
          title: title.trim(),
          whatsapp_link: link.trim(),
          user_id: userId,
        },
      ])

      if (error) throw error

      setTitle("")
      setLink("")
      setShowSuccess(true)

      toast({
        title: "¡Éxito!",
        description: "Tu chat ha sido publicado para todos los usuarios",
      })
    } catch (error) {
      console.error("Error creating chat:", error)
      setError("Error al publicar el chat. Inténtalo de nuevo.")
    } finally {
      setLoading(false)
    }
  }

  const deleteChat = async (chatId: string) => {
    try {
      const { error } = await supabase.from("quinceanera_chats").delete().eq("id", chatId).eq("user_id", userId)

      if (error) throw error

      toast({
        title: "Chat eliminado",
        description: "El chat ha sido eliminado correctamente",
      })
    } catch (error) {
      console.error("Error deleting chat:", error)
      toast({
        title: "Error",
        description: "No se pudo eliminar el chat",
        variant: "destructive",
      })
    }
  }

  const openWhatsAppLink = (link: string) => {
    window.open(link, "_blank")
  }

  const getPaginatedChats = (chatList: Chat[], page: number) => {
    const startIndex = (page - 1) * CHATS_PER_PAGE
    const endIndex = startIndex + CHATS_PER_PAGE
    return chatList.slice(startIndex, endIndex)
  }

  const getTotalPages = (chatList: Chat[]) => {
    return Math.ceil(chatList.length / CHATS_PER_PAGE)
  }

  const ChatCard = ({ chat, showMenu = false }: { chat: Chat; showMenu?: boolean }) => (
    <Card className="group hover:shadow-lg transition-all duration-300 hover:scale-105 bg-gradient-to-br from-pink-50 to-purple-50 border-2 border-pink-200 hover:border-pink-300">
      <CardContent className="p-4 relative">
        {showMenu && (
          <DropdownMenu>
            <DropdownMenuTrigger asChild>
              <Button
                variant="ghost"
                size="sm"
                className="absolute top-2 right-2 h-8 w-8 p-0 opacity-70 hover:opacity-100"
              >
                <MoreVertical className="h-4 w-4" />
              </Button>
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end">
              <DropdownMenuItem onClick={() => deleteChat(chat.id)} className="text-red-600 hover:text-red-700">
                <Trash2 className="h-4 w-4 mr-2" />
                Eliminar
              </DropdownMenuItem>
            </DropdownMenuContent>
          </DropdownMenu>
        )}

        <div className="cursor-pointer" onClick={() => setSelectedChat(chat)}>
          <div className="flex items-center gap-2 mb-3">
            <PartyPopper className="h-5 w-5 text-pink-500" />
            <h3 className="font-semibold text-gray-800 line-clamp-2">{chat.title}</h3>
          </div>

          <div className="flex items-center gap-2 text-sm text-gray-600 mb-3">
            <MessageCircle className="h-4 w-4" />
            <span>Grupo de WhatsApp</span>
          </div>

          <div className="text-xs text-gray-500">{new Date(chat.created_at).toLocaleDateString("es-MX")}</div>
        </div>
      </CardContent>
    </Card>
  )

  const PaginationControls = ({
    currentPage,
    totalPages,
    onPageChange,
  }: {
    currentPage: number
    totalPages: number
    onPageChange: (page: number) => void
  }) => (
    <div className="flex justify-center items-center gap-4 mt-8">
      <Button
        variant="outline"
        onClick={() => onPageChange(currentPage - 1)}
        disabled={currentPage === 1}
        className="flex items-center gap-2"
      >
        <ChevronLeft className="h-4 w-4" />
        Anterior
      </Button>

      <span className="text-sm text-gray-600">
        Página {currentPage} de {totalPages}
      </span>

      <Button
        variant="outline"
        onClick={() => onPageChange(currentPage + 1)}
        disabled={currentPage === totalPages}
        className="flex items-center gap-2"
      >
        Siguiente
        <ChevronRight className="h-4 w-4" />
      </Button>
    </div>
  )

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-50 to-yellow-100">
      {/* Header */}
      <header className="bg-gradient-to-r from-pink-500 via-purple-500 to-yellow-500 text-white shadow-lg">
        <div className="container mx-auto px-4 py-6">
          <div className="flex items-center gap-3">
            <PartyPopper className="h-8 w-8" />
            <div>
              <h1 className="text-3xl font-bold">Quinceañeras.MTY</h1>
              <p className="text-pink-100">Encuentra los mejores grupos de fiestas de quinceaños en Monterrey</p>
            </div>
          </div>
        </div>
      </header>

      {/* Status Alert */}
      <Alert className="mx-4 mt-4 border-green-200 bg-green-50">
        <Database className="h-4 w-4 text-green-600" />
        <AlertDescription className="text-green-800">
          <strong>🔥 En tiempo real:</strong> Los chats se comparten entre todos los usuarios al instante.
        </AlertDescription>
      </Alert>

      {/* Navigation */}
      <nav className="bg-white shadow-md sticky top-0 z-40">
        <div className="container mx-auto px-4">
          <div className="flex space-x-8">
            {[
              { id: "upload", label: "Subir tu Chat", icon: MessageCircle },
              { id: "all", label: "Todos los Chats", icon: Users },
              { id: "my", label: "Mis Chats", icon: PartyPopper },
            ].map(({ id, label, icon: Icon }) => (
              <button
                key={id}
                onClick={() => setActiveTab(id as any)}
                className={`flex items-center gap-2 py-4 px-2 border-b-2 transition-colors ${
                  activeTab === id
                    ? "border-pink-500 text-pink-600"
                    : "border-transparent text-gray-600 hover:text-pink-500"
                }`}
              >
                <Icon className="h-5 w-5" />
                {label}
              </button>
            ))}
          </div>
        </div>
      </nav>

      {/* Content */}
      <main className="container mx-auto px-4 py-8">
        {activeTab === "upload" && (
          <div className="max-w-2xl mx-auto">
            <Card className="bg-white shadow-xl border-2 border-pink-200">
              <CardContent className="p-8">
                <div className="text-center mb-6">
                  <PartyPopper className="h-12 w-12 text-pink-500 mx-auto mb-4" />
                  <h2 className="text-2xl font-bold text-gray-800 mb-2">Subir tu Chat</h2>
                  <p className="text-gray-600">Comparte tu grupo de WhatsApp de quinceaños</p>
                </div>

                <form onSubmit={handleSubmit} className="space-y-6">
                  <div>
                    <Label htmlFor="title" className="text-gray-700 font-medium">
                      Título de la fiesta
                    </Label>
                    <Input
                      id="title"
                      value={title}
                      onChange={(e) => setTitle(e.target.value)}
                      placeholder="Ej: Quinceaños de María - Sábado 15 de Diciembre"
                      className="mt-2 border-pink-200 focus:border-pink-500"
                      disabled={loading}
                    />
                  </div>

                  <div>
                    <Label htmlFor="link" className="text-gray-700 font-medium">
                      Link del grupo de WhatsApp
                    </Label>
                    <Input
                      id="link"
                      value={link}
                      onChange={(e) => setLink(e.target.value)}
                      placeholder="https://chat.whatsapp.com/..."
                      className="mt-2 border-pink-200 focus:border-pink-500"
                      disabled={loading}
                    />
                  </div>

                  {error && (
                    <div className="bg-red-50 border border-red-200 text-red-700 px-4 py-3 rounded-lg text-sm">
                      {error}
                    </div>
                  )}

                  <Button
                    type="submit"
                    disabled={loading}
                    className="w-full bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600 text-white font-semibold py-3"
                  >
                    {loading ? (
                      <>
                        <Loader2 className="h-5 w-5 mr-2 animate-spin" />
                        Publicando...
                      </>
                    ) : (
                      <>
                        <MessageCircle className="h-5 w-5 mr-2" />
                        Publicar Chat
                      </>
                    )}
                  </Button>
                </form>
              </CardContent>
            </Card>
          </div>
        )}

        {activeTab === "all" && (
          <div>
            <div className="text-center mb-8">
              <h2 className="text-3xl font-bold text-gray-800 mb-2">Todos los Chats</h2>
              <p className="text-gray-600">Descubre las mejores fiestas de quinceaños en Monterrey</p>
              <p className="text-sm text-gray-500 mt-2">Total: {chats.length} grupos disponibles</p>
            </div>

            {chats.length === 0 ? (
              <div className="text-center py-12">
                <PartyPopper className="h-16 w-16 text-gray-400 mx-auto mb-4" />
                <p className="text-gray-500 text-lg">No hay chats disponibles aún</p>
                <p className="text-gray-400">¡Sé el primero en compartir un grupo!</p>
              </div>
            ) : (
              <>
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                  {getPaginatedChats(chats, allChatsPage).map((chat) => (
                    <ChatCard key={chat.id} chat={chat} />
                  ))}
                </div>

                {getTotalPages(chats) > 1 && (
                  <PaginationControls
                    currentPage={allChatsPage}
                    totalPages={getTotalPages(chats)}
                    onPageChange={setAllChatsPage}
                  />
                )}
              </>
            )}
          </div>
        )}

        {activeTab === "my" && (
          <div>
            <div className="text-center mb-8">
              <h2 className="text-3xl font-bold text-gray-800 mb-2">Mis Chats</h2>
              <p className="text-gray-600">Administra los grupos que has compartido</p>
              <p className="text-sm text-gray-500 mt-2">Tienes {myChats.length} grupos publicados</p>
            </div>

            {myChats.length === 0 ? (
              <div className="text-center py-12">
                <MessageCircle className="h-16 w-16 text-gray-400 mx-auto mb-4" />
                <p className="text-gray-500 text-lg">No has subido ningún chat aún</p>
                <Button
                  onClick={() => setActiveTab("upload")}
                  className="mt-4 bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600"
                >
                  Subir mi primer chat
                </Button>
              </div>
            ) : (
              <>
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                  {getPaginatedChats(myChats, myChatsPage).map((chat) => (
                    <ChatCard key={chat.id} chat={chat} showMenu={true} />
                  ))}
                </div>

                {getTotalPages(myChats) > 1 && (
                  <PaginationControls
                    currentPage={myChatsPage}
                    totalPages={getTotalPages(myChats)}
                    onPageChange={setMyChatsPage}
                  />
                )}
              </>
            )}
          </div>
        )}
      </main>

      {/* Success Modal */}
      <Dialog open={showSuccess} onOpenChange={setShowSuccess}>
        <DialogContent className="sm:max-w-md">
          <DialogHeader>
            <DialogTitle className="text-center text-green-600 flex items-center justify-center gap-2">
              <PartyPopper className="h-6 w-6" />
              ¡Chat subido con éxito!
            </DialogTitle>
          </DialogHeader>
          <div className="text-center py-4">
            <p className="text-gray-600 mb-4">
              Tu grupo de WhatsApp ha sido publicado y ya está visible para todos los usuarios.
            </p>
            <Button
              onClick={() => setShowSuccess(false)}
              className="bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600"
            >
              Aceptar
            </Button>
          </div>
        </DialogContent>
      </Dialog>

      {/* Chat Detail Modal */}
      <Dialog open={!!selectedChat} onOpenChange={() => setSelectedChat(null)}>
        <DialogContent className="sm:max-w-lg">
          {selectedChat && (
            <>
              <DialogHeader>
                <DialogTitle className="flex items-center gap-2 text-xl">
                  <PartyPopper className="h-6 w-6 text-pink-500" />
                  {selectedChat.title}
                </DialogTitle>
              </DialogHeader>
              <div className="py-4">
                <div className="bg-gradient-to-r from-pink-50 to-purple-50 p-6 rounded-lg mb-6">
                  <div className="flex items-center gap-2 mb-4">
                    <MessageCircle className="h-5 w-5 text-pink-500" />
                    <span className="font-medium text-gray-700">Grupo de WhatsApp</span>
                  </div>
                  <p className="text-sm text-gray-600 mb-4">
                    Publicado el{" "}
                    {new Date(selectedChat.created_at).toLocaleDateString("es-MX", {
                      year: "numeric",
                      month: "long",
                      day: "numeric",
                    })}
                  </p>
                </div>

                <div className="flex gap-3">
                  <Button
                    onClick={() => openWhatsAppLink(selectedChat.whatsapp_link)}
                    className="flex-1 bg-green-500 hover:bg-green-600 text-white"
                  >
                    <ExternalLink className="h-4 w-4 mr-2" />
                    Unirse al Grupo
                  </Button>
                  <Button variant="outline" onClick={() => setSelectedChat(null)}>
                    Cerrar
                  </Button>
                </div>
              </div>
            </>
          )}
        </DialogContent>
      </Dialog>
    </div>
  )
}
