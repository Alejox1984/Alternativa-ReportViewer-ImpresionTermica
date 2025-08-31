# Alternativa-ReportViewer-ImpresionTermica
Solución técnica para impresión térmica en WinForms sin depender de ReportViewer. Layout físico preciso, impresión directa y lógica desacoplada.
# Alternativa técnica a ReportViewer para impresión térmica en WinForms: precisión y control

## Introducción

En entornos donde la fidelidad visual es crítica —como la impresión térmica de etiquetas— ReportViewer no siempre ofrece resultados consistentes. Distorsiones en el layout, pérdida de padding y falta de control sobre el render final son problemas frecuentes. Esta alternativa técnica propone una solución directa, sin dependencias externas, que permite controlar el diseño físico de forma precisa y reproducible.

## Contexto técnico

ReportViewer fue diseñado para generar reportes visuales, pero su comportamiento al imprimir en dispositivos térmicos no garantiza coherencia entre lo que se muestra en pantalla y lo que se imprime. En escenarios donde el layout debe respetar márgenes, espaciado y fuente al milímetro, esta herramienta no cumple con los requisitos.

La solución presentada evita rehacer el trabajo ya realizado. En lugar de adaptar ReportViewer, se construye un flujo propio de navegación, vista previa e impresión, manteniendo la lógica de negocio y respetando el diseño físico.

## Componentes de la solución

### 1. Navegador de paginación personalizado
- Componente con cinco botones (Primero, Anterior, Página actual [TextBox], Siguiente, Último).
- Lógica desacoplada del ecosistema ReportViewer.
- Sin adornos ni dependencias externas.

### 2. Formulario de vista previa
- Panel superior con `Dock.Top`, encapsulado en `TableLayoutPanel` para evitar distorsión al maximizar.
- Panel inferior con `PictureBox` que renderiza la etiqueta como imagen.

### 3. Impresión directa
- Botón "Imprimir" lanza `PrintDialog`.
- Se obtienen parámetros del usuario (impresora, tamaño, orientación).
- Se dibuja la etiqueta con GDI+, respetando el layout visual.
- Se imprime directamente, sin reinterpretaciones.

## Adaptación para otros proyectos

La lógica de impresión está encapsulada en el componente de navegación. Para integrarla:

- Adaptar la entidad a tu modelo de datos.
- Mapear los campos relevantes al layout visual.
- Respetar el diseño físico definido en código.

Ejemplo de entidad genérica:

```csharp
public class EtiquetaTermica
{
    public string NombreProducto { get; set; }
    public string Codigo { get; set; }
    public DateTime Fecha { get; set; }
    public string Lote { get; set; }
    public string Ubicacion { get; set; }
}
