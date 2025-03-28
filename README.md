# 🎙️ Voice-to-Code

**Status:** 🚧 Work in Progress  
**Type:** Prompt-to-Code Experiment / Full-Stack via Voice / Cursor Playground  

---

## 🧠 What This Is

This project explores whether a **full-stack app can be built entirely through spoken logic**.

Using ChatGPT's **speech-to-text**, I describe every piece of the app — structure, logic, flow — *out loud*. ChatGPT turns that into a detailed prompt, which is then passed into **Cursor** to generate frontend and backend code.

It’s not casual conversation — I’m speaking in pure dev logic, like:

> “When the TaskBoard loads, fetch all TaskLists from the backend and render each one in a horizontally scrollable column. Add a button to create a new TaskList that sends a POST request and updates the layout immediately.”

This becomes the blueprint. No boilerplate, no typing — just **thought → instruction → implementation**.

---

## 💡 Why I'm Doing This

- To **think in logic**, speak in code, and skip the keyboard.
- To treat **prompting as a legitimate engineering skill**.
- To see if **natural speech** improves speed and clarity.
- To explore how far **Cursor + GPT** can go with precise direction.

---

## 📌 Current Focus: Leo (Second Brain)

Leo isn’t a fixed product. It’s a space to:
- Stay productive 
- Keep things in flow 
- Track thoughts, tasks, and time 
- Evolve based on whatever I need — or feel like experimenting with

Sometimes it’s about refining a feature. 
Other times it’s about testing strange combinations, mixing concepts, and seeing what happens.

The backend is still changing — I’m tweaking functionality, debugging as I go, and refining the logic one step at a time.

There’s no roadmap — just exploration, iteration, and fun.

Eventually, Leo will include an AI component — but what it *does* will depend entirely on the structure and data we build along the way.

---

## 🔁 Development Process

All development is **prompt-driven**, from start to finish.

1. I **speak** the full logic — layout, state, backend, interactions.
2. ChatGPT **transcribes and refines** the logic into a clean prompt.
3. I **paste** the prompt into Cursor.
4. Code is **generated**, and I **iterate** only through more spoken logic.

> No manual typing. No boilerplate. No edits unless debugging.

---

## 🧪 Prompting Styles

We use two styles of prompts depending on the task:

---

### 1. 🎨 Natural Prompt – Styling & Design

Example:

> **Rebuild the TaskBoard UI** in a clean, minimal way using the current file structure.  
> Do not create new components unless necessary.

**✅ Core Functionality:**
- Fetch and render all `TaskLists` from MySQL backend
- Use real backend API (TRPC or REST)
- Render each list as a **glassmorphic vertical column**
- Add a `+ Add List` button:
  - Sends a POST request to create new TaskList
  - Appends the new list to the board immediately
- No drag-and-drop yet – just a simple flex layout

**✅ Visual Design:**
- Background: **Starry Night Gradient**
  - `from-indigo-900 via-sky-800 to-sky-700`
- List Cards:
  - `bg-white/20 backdrop-blur-md rounded-xl p-4 shadow-lg text-white`
- Header:
  - Centered gradient text: **“Task Board”**

---

### 2. 🧠 Logic-Heavy Prompt – Functionality Bug Fix

**Fix the task deletion bug** where the first attempt fails with `"Task not found"` but the second attempt works.

**✅ Problem:**
- Clicking “Delete” gives: `Task not found`
- Works on retry

**✅ Root Cause:**
- UI updates optimistically *before* backend deletion is confirmed
- `taskId` might be stale or missing

**✅ Required Fix:**

1. Disable Optimistic Deletion
- Do not remove the task from state until the backend confirms success

2. Confirm Task ID
```ts
if (!taskId) {
  console.warn("No task ID provided to delete");
  return;
}
```

3. Await the Delete Mutation
```ts
try {
  await deleteTask({ id });
  setTasks(prev => prev.filter(t => t.id !== id));
} catch (error) {
  showErrorToast("Failed to delete task. Try again.");
}
```

4. Ensure Fresh State
- Check that task IDs are passed correctly through props
- Avoid stale component references
  
**✅ Result:**
- Task deletes immediately on first attempt
- No error toast unless there’s a real backend failure

## 📸 Visual Progress


https://github.com/user-attachments/assets/35fb75b2-7ce2-4bc3-b1ac-1d3aaa5672c3




## 🛠️ Tech Stack

### 🧩 Frontend
- **Next.js**
- **React**
- **TypeScript**
- **TailwindCSS**
- **Framer Motion** – Animations
- **DND Kit** – Drag and Drop functionality
- **Lucide React** – Icon library

### 🛠️ Backend
- **Next.js API Routes**
- **Prisma** – ORM
- **TypeScript**

### ⚙️ Tooling & Infrastructure
- **TypeScript**
- **ESLint** – Linting
- **PostCSS** + **Autoprefixer** – Styling tools
- **Git**
- **npm** – Package management

## 🗣️ Final Thought

This project is a simple experiment:

Can we build real software just by speaking it into existence?

So far, the answer feels like yes. 
