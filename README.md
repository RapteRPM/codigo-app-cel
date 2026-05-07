# codigo-app-cel

LOGIN
POST /api/login
Content-Type: application/json

Request:
{
  "email": "sebastian@rpm.com",
  "password": "sebastian123"
}

Response (200):
{
  "success": true,
  "message": "Login exitoso",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "usuario": {
    "IdUsuario": 72001,
    "TipoUsuario": "Comerciante",
    "Nombre": "Sebastian",
    "Apellido": "Mora",
    "Correo": "sebastian@rpm.com",
    "Telefono": "3007200001",
    "NombreComercio": "Comercio Sebastian",
    "Direccion": "Cra 2 # 2-02",
    "Latitud": 7.8895,
    "Longitud": -72.4967,
    "Barrio": "Centro",
    "NitComercio": 8001001
  }
}

REGISTRO
POST /api/register
Content-Type: application/json

Request:
{
  "tipoUsuario": "Comerciante",
  "nombre": "Juan",
  "apellido": "Perez",
  "documento": "1234567890",
  "telefono": "3001234567",
  "email": "juan@rpm.com",
  "password": "Password123@",
  "nombreComercio": "Moto Repuestos Juan",
  "direccion": "Calle 5 # 10-20",
  "barrio": "Centro",
  "latitud": 7.8895,
  "longitud": -72.4967,
  "nitComercio": 9999001,
  "redesSociales": "@motos_juan",
  "diasAtencion": "Lunes-Sabado",
  "horaInicio": "08:00:00",
  "horaFin": "18:00:00"
}

Response (201):
{
  "success": true,
  "message": "Registro exitoso. Por favor verifica tu email",
  "registroId": 98001,
  "token": "tok_98001_xxx"
}

PUBLICAR SERVICIO
POST /api/publicaciones
Content-Type: application/json
Authorization: Bearer {token}

Request:
{
  "nombreProducto": "Casco Integral Premium",
  "descripcion": "Casco de seguridad certificado, talla M",
  "categoria": 1,  // 1=Accesorios, 2=Repuestos, 3=Servicio mecanico, 4=Servicio de grua
  "precio": 250000,
  "stock": 15,
  "imagenProducto": "base64_encoded_image_or_url"
}

Response (201):
{
  "success": true,
  "message": "Publicación creada exitosamente",
  "publicacionId": 84001,
  "publicacion": {
    "IdPublicacion": 84001,
    "NombreProducto": "Casco Integral Premium",
    "Descripcion": "Casco de seguridad certificado, talla M",
    "Categoria": 1,
    "Precio": 250000,
    "Stock": 15,
    "ImagenProducto": "...",
    "FechaPublicacion": "2026-05-06T14:30:00Z"
  }
}

OBTENER PUBLICACIONES
GET /api/mis-publicaciones
Authorization: Bearer {token}

Response (200):
{
  "success": true,
  "data": [
    {
      "IdPublicacion": 84001,
      "NombreProducto": "Casco Integral",
      "Descripcion": "Casco certificado",
      "Categoria": 1,
      "NombreCategoria": "Accesorios",
      "Precio": 250000,
      "Stock": 10,
      "ImagenProducto": "casco.jpg",
      "FechaPublicacion": "2026-05-06T10:00:00Z",
      "VentasTotal": 3
    },
    {
      "IdPublicacion": 84002,
      "NombreProducto": "Cambio de Aceite",
      "Descripcion": "Servicio completo",
      "Categoria": 3,
      "NombreCategoria": "Servicio mecanico",
      "Precio": 80000,
      "Stock": 50,
      "ImagenProducto": "aceite.jpg",
      "FechaPublicacion": "2026-05-06T11:00:00Z",
      "VentasTotal": 5
    }
  ]
}

EDITAR PUBLICACION
PUT /api/publicaciones/{publicacionId}
Content-Type: application/json
Authorization: Bearer {token}

Request:
{
  "nombreProducto": "Casco Integral Premium v2",
  "descripcion": "Casco actualizado",
  "precio": 260000,
  "stock": 20,
  "imagenProducto": "base64_or_url"
}

Response (200):
{
  "success": true,
  "message": "Publicación actualizada",
  "publicacion": { ... }
}

ELIMINAR PUBLICACION
DELETE /api/publicaciones/{publicacionId}
Authorization: Bearer {token}

Response (200):
{
  "success": true,
  "message": "Publicación eliminada"
}

AGENDA DE SERVICIOS
GET /api/mis-ordenes
Authorization: Bearer {token}

Response (200):
{
  "success": true,
  "data": [
    {
      "IdDetalleFactura": 91001,
      "IdFactura": 90001,
      "NombreProducto": "Casco Integral",
      "Cantidad": 1,
      "PrecioUnitario": 250000,
      "Total": 250000,
      "UsuarioComprador": "Daniel Lopez",
      "UsuarioId": 71001,
      "FechaCompra": "2026-05-06T10:00:00Z",
      "Estado": "Pendiente",
      "MetodoPago": "Efectivo"
    }
  ]
}

ACTUALIZAR ESTADO DE ORDEN
PUT /api/ordenes/{detalleFacturaId}/estado
Content-Type: application/json
Authorization: Bearer {token}

Request:
{
  "estado": "Entregado"  // o "Pendiente", "Cancelado"
}

Response (200):
{
  "success": true,
  "message": "Estado actualizado a Entregado"
}

OBTENER CATEGORIA
GET /api/categorias

Response (200):
{
  "success": true,
  "data": [
    { "IdCategoria": 1, "NombreCategoria": "Accesorios" },
    { "IdCategoria": 2, "NombreCategoria": "Repuestos" },
    { "IdCategoria": 3, "NombreCategoria": "Servicio mecanico" },
    { "IdCategoria": 4, "NombreCategoria": "Servicio de grua" }
  ]
}

OBTENER PERFIL COMERCIANTE
GET /api/perfil-comerciante
Authorization: Bearer {token}

Response (200):
{
  "success": true,
  "comerciante": {
    "NitComercio": 8001001,
    "NombreComercio": "Comercio Sebastian",
    "Direccion": "Cra 2 # 2-02",
    "Latitud": 7.8895,
    "Longitud": -72.4967,
    "Barrio": "Centro",
    "RedesSociales": "@sebastianrpm",
    "DiasAtencion": "Lunes-Sabado",
    "HoraInicio": "08:00:00",
    "HoraFin": "18:00:00",
    "TotalVentas": 15,
    "CalificacionPromedio": 4.5
  }
}

ESTRUCTURA DE RegisterResponse (Kotlin)

data class RegisterResponse(
    val success: Boolean,
    val message: String,
    val registroId: Int? = null,
    val token: String? = null
)

data class LoginResponse(
    val success: Boolean,
    val message: String,
    val token: String? = null,
    val usuario: UsuarioData? = null
)

data class UsuarioData(
    val IdUsuario: Int,
    val TipoUsuario: String,
    val Nombre: String,
    val Apellido: String,
    val Correo: String,
    val Telefono: String,
    val NombreComercio: String,
    val Direccion: String,
    val NitComercio: Int
)

data class PublicacionResponse(
    val success: Boolean,
    val message: String,
    val publicacionId: Int? = null,
    val publicacion: Publicacion? = null
)

data class Publicacion(
    val IdPublicacion: Int,
    val NombreProducto: String,
    val Descripcion: String,
    val Categoria: Int,
    val Precio: Double,
    val Stock: Int,
    val ImagenProducto: String,
    val FechaPublicacion: String
)

Ten en cuenta que quiza y no todo se use en esta app
