# Token
Trabajo de Token en CSS por Lara Veloso, Xavier Lacunza y Franco Talavera
# Sistema de Design Tokens — Modelo de 3 Capas

Este repositorio contiene la implementación de un sistema de Design Tokens estructurado en un modelo de tres capas (token tiering), diseñado para mantener una arquitectura visual escalable, consistente y mantenible.


1. Arquitectura del Sistema (3 Capas)

El flujo de referencias va estrictamente de abajo hacia arriba: los componentes nunca consumen primitivos directamente.

- Capa 1 — Primitivos (`styles/tokens/_primitives.css`):
  Almacena los valores crudos (*raw values*) de color, espaciado, radios y tipografía. No definen ningún propósito o intencionalidad de uso.
  *Ejemplo:* `--color-blue-500: #046bd2;`

- Capa 2 — Semánticos (`styles/tokens/_semantic.css`):
  Asigna la intención de uso o rol funcional a los valores primitivos. Aquí es donde habita la lógica de temas (Modo Claro / Modo Oscuro).
  Ejemplo: `--color-action: var(--color-blue-500);`

- Capa 3 — Componente (`styles/tokens/_component.css`):
  Tokens específicos para la interfaz de un widget o componente particular. Consumen exclusivamente tokens semánticos (Capa 2).
  *Ejemplo:* `--button-bg: var(--color-action);`

---

 2. Cadenas de Trazabilidad de Tokens

A continuación se muestra la cadena completa de referencia desde el valor crudo hasta la aplicación final en el componente:

text
[Capa 1: Primitives]         [Capa 2: Semantic]           [Capa 3: Component]        [Componente CSS]
--color-blue-500 (#046bd2) ──► --color-action ──────────────► --button-bg ─────────────► background-color: var(--button-bg);
--radius-md (8px) ─────────► --border-radius-default ─────► --button-radius ─────────► border-radius: var(--button-radius);

---

3. El cambio de tema se logra modificando únicamente la Capa 2 (_semantic.css), manteniendo intactos los valores primitivos y las referencias de los componentes.

Para alternar entre temas, el proyecto aplica el atributo data-theme="dark" en el elemento :root:

---

4. Citas de Autoridad
"Design tokens are the visual design atoms of the design system — specifically, they are named entities that store visual design attributes. We use them in place of hard-coded values (such as hex values for color or pixel values for spacing) in order to maintain a scalable and consistent visual system for UI development."— Salesforce, Design Tokens, Lightning Design System.   "I chose not to release this CSS reset as an NPM package because I feel like you should own your reset."— Comeau, J. W. (2021), A Modern CSS Reset.
