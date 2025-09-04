# Cartao-Digital-de-Identificacao

**Projeto de Avaliação Formadora 1 – Módulo de Programação Móvel da Faculdade**

Aplicação moderna construída com **Ionic + Angular** que apresenta um **cartão digital de identificação** (Home) e uma tela **Sobre**. O foco é praticar estrutura de projeto, navegação, responsividade e estilização em apps móveis híbridos.

---

## Telas

- **Cartão Digital (Home)**  
  Exibe foto de perfil, nome e **Código da Turma** (rótulo + chip centralizados).  
  Possui botão **Sobre** para navegar à segunda tela.

- **Sobre**  
  Texto curto e receptivo de apresentação e botão **Voltar à tela inicial**.

O visual reutiliza gradiente, “glass card”, avatar circular com aro em degradê, blobs suaves ao fundo, dark mode e tamanhos fluídos com `clamp()`.

---

## Tecnologias

- Ionic Framework (Angular)
- Angular
- SCSS/CSS moderno (`color-mix`, `clamp`, `backdrop-filter`)
- (opcional) Capacitor para Android/iOS

---

## Requisitos

- **Node.js** 18+ (recomendado)
- **Ionic CLI** global

```bash
npm i -g @ionic/cli

```

Instalação & Execução
bash
Copiar código

# Instalar dependências

```bash
npm install
```

# Rodar em modo dev (http://localhost:8100)

```bash
ionic serve
```

Android / iOS (opcional, via Capacitor)

```bash
# Build web
ionic build


# Adicionar plataforma
ionic cap add android
ionic cap add ios

# Abrir projeto nativo
ionic cap open android
ionic cap open ios
```

# Estrutura do Projeto

> Arquitetura padrão: páginas dentro de src/app.

```bash
src/
└─ app/
   ├─ cartao-digital/
   │  ├─ cartao-digital.page.html
   │  ├─ cartao-digital.page.scss
   │  └─ cartao-digital.page.ts
   ├─ about/
   │  ├─ about.page.html
   │  ├─ about.page.scss
   │  └─ about.page.ts
   ├─ app.routes.ts              # (projetos standalone)
   └─ app-routing.module.ts      # (projetos com módulos)
assets/
└─ perfil.jpg
```

# Rotas

> Escolha o bloco conforme seu projeto: standalone (Angular moderno, sem módulos) ou com módulos.

> Standalone (src/app/app.routes.ts)

```bash
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: '',
    loadComponent: () =>
      import('./cartao-digital/cartao-digital.page').then(m => m.CartaoDigitalPage),
  },
  {
    path: 'about',
    loadComponent: () =>
      import('./about/about.page').then(m => m.AboutPage),
  },
];
```

> Com módulos (src/app/app-routing.module.ts)

```bash
import { NgModule } from '@angular/core';
import { PreloadAllModules, RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  {
    path: '',
    loadChildren: () =>
      import('./cartao-digital/cartao-digital.module').then(m => m.CartaoDigitalPageModule),
  },
  {
    path: 'about',
    loadChildren: () =>
      import('./about/about.module').then(m => m.AboutPageModule),
  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules })],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

# Navegação pelos botões

```bash
<!-- Home -->
<ion-button routerLink="/about">Sobre</ion-button>

<!-- About -->
<ion-button fill="outline" routerLink="/">Voltar à tela inicial</ion-button>
```

# Assets (Imagem de Perfil)

> Coloque sua imagem em src/assets/perfil.jpg.
> Use no HTML:

```bash
<img alt="Foto de perfil" src="assets/perfil.jpg" />
```

> Verifique no angular.json se os assets estão configurados:

```bash
{
  "assets": ["src/favicon.ico", "src/assets"]
}
```

# Estilo & Tema

> Ajuste os tokens no :host para alterar a paleta de cores:

```bash
:host {
  --accent-1: hsl(200 90% 55%);
  --accent-2: hsl(160 70% 48%);
  --text-strong: hsl(220 20% 15%);
  --text-muted: hsl(220 10% 45%);
}
```

# Destaques de UI

- Card translúcido com backdrop-filter.
- Avatar circular com aro em degradê (conic-gradient).
- Responsividade real com clamp() (tamanhos e espaçamentos).
- Dark mode automático (prefers-color-scheme: dark).
- Fundo dinâmico com blobs suaves (desativados por prefers-reduced-motion).
- “Código da Turma” centralizado (rótulo + chip com ícone e texto).

# Conteúdo de Exemplo — Tela Sobre

- Nome: Victor Hugo Inacio de Oliveira
- Idade: 22 anos
- Curso: Análise e Desenvolvimento de Sistemas — UNISUAM (4º módulo)
- Experiência: Estagiário na Petronect
- Interesses: tecnologia em áreas diversas, criar projetos e aprender coisas novas continuamente.

> O texto é curto, receptivo e mantém o padrão visual da Home.

# Gerar novas páginas (opcional)

```bash
ionic g page about

# ou:
ionic g page pages/minha-nova-pagina
```

> Depois, registre a rota conforme a seção Rotas.

# Solução de Problemas

> Imagem não aparece

1. Caminho correto no HTML: src="assets/perfil.jpg".

2. angular.json contém "src/assets" em assets.

3. Z-index no avatar:

```bash
.avatar-ring::after { z-index: 0; }
.avatar-ring img { z-index: 1; }
```

4. Faça Hard Reload (Ctrl/Cmd + Shift + R).

# Estilos não aplicam

> Pode ser encapsulamento de estilos do Angular. Como último recurso:

```bash
:host ::ng-deep ion-card-content { /* suas regras aqui */ }
```

# Acessibilidade

- Bom contraste (light/dark).
- Animações respeitam prefers-reduced-motion.
- Imagem com alt descritivo.

# Licença

- Uso acadêmico/educacional (Projeto de Avaliação Formadora 1 – Módulo de Programação Móvel da Faculdade).
- Adapte a licença conforme necessário (ex.: MIT).
