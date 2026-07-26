<div align="center">

# Smart Workplace AI Hub

Workspace productivity app berbasis Next.js yang menggabungkan AI chat assistant, task automation, dan knowledge base pribadi — dibangun dengan RAG pipeline dan native function calling dari Gemini API.

[![Next.js](https://img.shields.io/badge/next%20js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
[![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Shadcn UI](https://img.shields.io/badge/shadcn%2Fui-000000?style=for-the-badge&logo=shadcnui&logoColor=white)](https://ui.shadcn.com/)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)
[![Gemini API](https://img.shields.io/badge/Gemini%20API-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=for-the-badge)](./LICENSE)

[🚀 Live Demo](https://[link-demo-kamu].com) · [🐛 Report Bug](https://github.com/mhmdrehaan/[repo-name]/issues) · [✨ Request Feature](https://github.com/mhmdrehaan/[repo-name]/issues)

</div>

<br />

<div align="center">
  <img src="./public/screenshot.png" alt="Smart Workplace AI Hub Screenshot" width="80%" />
  <br />
  <sub>[Ganti gambar di atas dengan screenshot/GIF demo dashboard atau AI chat panel — taruh filenya di folder /public]</sub>
</div>

<br />

---

## 📋 Daftar Isi

- [Key Features](#-key-features)
- [Tech Stack](#️-tech-stack)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Project Structure](#-project-structure)
- [Roadmap](#️-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Key Features

- 🤖 **AI Chat Assistant** — Chat panel dengan native Gemini function calling (`FunctionDeclarationsTool`), bisa manggil tools secara otomatis berdasarkan konteks percakapan
- 📚 **RAG-Powered Knowledge Base** — Retrieval-Augmented Generation via Supabase vector search RPC (`match_documents`), dengan dynamic retrieval depth (5 chunks untuk lookup query, sampai 15 chunks untuk aggregation query)
- ✅ **Task Automation via AI** — AI bisa langsung `create_task` dari chat, lengkap dengan assignment ke user tertentu (`assignee_id`)
- 🔐 **Auth & Access Control** — Autentikasi user menggunakan Supabase Auth
- 🚦 **Guest Rate Limiting** — Pembatasan request untuk guest user menggunakan Upstash Redis, biar API gak gampang di-abuse
- 📊 **Dashboard Analytics** — Visualisasi data & activity overview di satu halaman dashboard
- 🧠 **Smart Context Handling** — Truncation & context note injection biar AI tetap aware kalau jawaban yang dikasih cuma sebagian dari data yang ada

> 💡 Fitur di atas sudah disesuaikan dengan progress terakhir — update lagi kalau ada penambahan (misal WhatsApp notification via Fonnte/Wablas/Twilio/Meta Cloud API yang lagi dieksplor).

---

## 🛠️ Tech Stack

**Frontend**
- [Next.js](https://nextjs.org/) — React framework dengan App Router
- [React.js](https://react.dev/) — UI library
- [TypeScript](https://www.typescriptlang.org/) — Type-safe development

**Styling / UI**
- [Tailwind CSS](https://tailwindcss.com/) — Utility-first CSS
- [Shadcn UI](https://ui.shadcn.com/) — Komponen UI yang customizable

**Backend / Database**
- [Supabase](https://supabase.com/) — PostgreSQL, Auth, dan Vector Store (pgvector) buat RAG
- [Gemini API](https://ai.google.dev/) — LLM & native function calling engine

**Infrastructure / Tools**
- [Upstash](https://upstash.com/) — Redis untuk rate limiting guest user
- [Git](https://git-scm.com/) & [GitHub](https://github.com/) — Version control
- [Vercel](https://vercel.com/) — Hosting & deployment

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) `v18.x` atau lebih baru
- [npm](https://www.npmjs.com/) / [yarn](https://yarnpkg.com/) / [pnpm](https://pnpm.io/)
- [Git](https://git-scm.com/)
- Akun [Supabase](https://supabase.com/) (dengan pgvector extension aktif buat RAG)
- API key dari [Google AI Studio](https://aistudio.google.com/) buat Gemini API
- Akun [Upstash](https://upstash.com/) (buat rate limiting)

### Installation

**1. Clone repository ini**

```bash
git clone https://github.com/mhmdrehaan/[repo-name].git
cd [repo-name]
```

**2. Install dependencies**

```bash
npm install
# atau
yarn install
# atau
pnpm install
```

**3. Setup environment variables**

```bash
cp .env.example .env.local
```

Isi sesuai konfigurasi kamu — lihat bagian [Environment Variables](#-environment-variables) di bawah.

**4. Setup database Supabase**

Jalankan migration/schema SQL kamu di Supabase SQL Editor, termasuk function `match_documents` buat vector search RAG.

**5. Jalankan development server**

```bash
npm run dev
# atau
yarn dev
# atau
pnpm dev
```

Buka [http://localhost:3000](http://localhost:3000) — dashboard dan AI chat panel siap dipakai! 🎉

**6. Build untuk production (opsional)**

```bash
npm run build
npm run start
```

---

## 🔑 Environment Variables

Bikin file `.env.local` di root project:

```env
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Supabase
NEXT_PUBLIC_SUPABASE_URL=[your-supabase-project-url]
NEXT_PUBLIC_SUPABASE_ANON_KEY=[your-supabase-anon-key]
SUPABASE_SERVICE_ROLE_KEY=[your-supabase-service-role-key]

# Gemini AI
GEMINI_API_KEY=[your-gemini-api-key]

# Upstash Rate Limiting (guest access)
UPSTASH_REDIS_REST_URL=[your-upstash-redis-url]
UPSTASH_REDIS_REST_TOKEN=[your-upstash-redis-token]

# [Tambahan kalau udah pilih provider WhatsApp notification]
# WHATSAPP_PROVIDER=[fonnte/wablas/twilio/meta]
# WHATSAPP_API_KEY=[your-api-key]
```

> ⚠️ **Penting:** Jangan commit `.env.local` ke repo. Pastiin sudah masuk `.gitignore`.

---

## 📁 Project Structure

```
smart-workplace-ai-hub/
├── app/
│   ├── (auth)/                # Halaman login/register (Supabase Auth)
│   ├── api/
│   │   ├── chat/              # Endpoint AI chat + function calling
│   │   └── tasks/             # Endpoint task automation
│   └── dashboard/             # Halaman dashboard analytics
├── components/
│   ├── ui/                    # Shadcn UI components
│   ├── chat/                  # Komponen AI chat panel
│   └── dashboard/              # Komponen dashboard & analytics
├── lib/
│   ├── supabase/               # Supabase client, queries, match_documents RPC
│   ├── ai/
│   │   ├── functions/          # Function declarations (create_task, dll)
│   │   └── rag.ts              # Logic RAG: retrieval depth, truncation, context note
│   └── ratelimit/               # Upstash rate limiter config
├── types/                      # TypeScript type definitions
├── public/                     # Static assets
├── .env.example
└── README.md
```

> Sesuaikan lagi kalau struktur folder aktual kamu berbeda ya, Hans.

---

## 🗺️ Roadmap

- [ ] Integrasi WhatsApp notification ke AI chat pipeline (masih milih antara Fonnte, Wablas, Twilio, atau Meta Cloud API)
- [ ] Dark mode toggle
- [ ] Export laporan dashboard ke PDF/Excel
- [ ] Unit & integration testing (Jest / Playwright)
- [ ] Multi-workspace support (kolaborasi tim)
- [ ] Notifikasi real-time via Supabase Realtime

---

## 🤝 Contributing

Kontribusi terbuka banget! Caranya:

1. Fork repository ini
2. Buat branch baru (`git checkout -b feature/FiturBaru`)
3. Commit perubahan (`git commit -m 'Add: FiturBaru'`)
4. Push ke branch (`git push origin feature/FiturBaru`)
5. Buka Pull Request

---

## 📄 License

Proyek ini dilisensikan di bawah [MIT License](./LICENSE).

---

<div align="center">

Dibuat dengan ❤️ oleh **Muhammad Yusuf Raihan**

[![Portfolio](https://img.shields.io/badge/Portfolio-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://hansdev.my.id/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/muhammad-yusuf-raihan/)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:mhmdrehaann4@gmail.com)

</div>
