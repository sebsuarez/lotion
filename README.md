# Lotion 📝

Lotion is a Notion-inspired note-taking web app built with React. Users can create, edit, view, and delete rich-text notes, with all data saved locally in the browser, so notes persist across sessions without a backend or database.

---

## ✨ Features

- **Create notes** instantly from the sidebar, each with a title, a date and time, and rich-text content
- **Rich-text editing** with formatting tools (bold, italics, lists, headings, and more) powered by React Quill
- **View and edit modes**, so notes open read-only and switch to an editor only when you choose to edit
- **Delete with confirmation**, preventing accidental loss of notes
- **Persistent storage**: notes are saved to `localStorage` and survive page refreshes and browser restarts
- **Collapsible sidebar** listing all notes with a title, date, and content preview for quick navigation
- **Readable timestamps**: raw `datetime-local` values are formatted into readable dates (e.g., "October 27, 2026, 2:30 PM")
- [**Searchable tags** with suggestions for existing tags as you type]
- [**Search and sorting** to quickly find notes]

---

## 🏗️ How It Works

### Routing
Lotion uses **React Router** for client-side routing, so each note has its own URL:

| Route | Purpose |
|---|---|
| `/notes` | Default view, with all notes in the sidebar |
| `/notes/:id` | View a single note (read-only) |
| `/notes/:id/edit` | Edit a note's title, date, and content |

A shared **layout route** renders the header and sidebar once, while the main panel swaps between view and edit pages using React Router's `<Outlet />`. Note data and update functions are passed to child routes through `useOutletContext`, and `useParams` reads the note ID from the URL to load the right note.

When a user saves an edit, `useNavigate` redirects them from `/notes/:id/edit` back to `/notes/:id`, so the app moves naturally between editing and reading.

### State Management
The app's state lives in React using **`useState`** for the list of notes and the current UI state. **`useEffect`** syncs that state with `localStorage`: notes load on startup and save automatically whenever they change. Each note gets a unique ID generated with the **`uuid`** library, which keeps routing and updates reliable.

### Data Persistence
Instead of a backend, Lotion stores everything in the browser's **`localStorage`** as JSON. This keeps the app fast and lightweight, and means it works entirely offline after loading.

### Layout & Styling
The interface is built with **CSS Flexbox**, using a fixed header, a collapsible sidebar, and a main content area, closely following Notion's clean design.

---

## 🛠️ Tech Stack

- **React** (hooks: `useState`, `useEffect`, `useRef`)
- **React Router** (`useParams`, `useNavigate`, `useOutletContext`, layout routes)
- **React Quill** for the rich-text editor
- **uuid** for unique note IDs
- **localStorage** for client-side persistence
- **HTML, CSS (Flexbox)**
- **Netlify** for deployment

---

## 🚀 Running Locally

```bash
git clone https://github.com/sebsuarez/notion-clone.git
cd lotion
npm install
npm start
```

The app will open at `http://localhost:3000`.

---

## 💡 What I Learned

- Structuring a multi-page React app with nested and layout routes
- Sharing state across routes without prop drilling using `useOutletContext`
- Persisting and syncing app state with browser storage
- Integrating a third-party rich-text editor into a React component tree
- Deploying a single-page application to Netlify
