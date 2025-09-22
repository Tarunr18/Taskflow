## TaskFlow — Behavior‑Driven Task Management (React + TypeScript)

TaskFlow is a modern task management app that combines intuitive Kanban workflows with behavioral analytics to help individuals and teams understand and improve how they work. It includes four core views: Kanban, Task List, Calendar, and Analytics.

### Highlights
- Kanban board with smooth drag‑and‑drop (To Do → In Progress → Review → Done)
- Task List with search, filters (status/priority/assignee), and sorting
- Calendar view showing tasks on due dates with priority/status indicators
- Analytics dashboard with charts (completion rate, status distribution, time by project) and behavioral insights (average session time, most active hour)
- Clean, responsive UI built with Tailwind CSS
- Type‑safe codebase with shared domain models

---

## Tech Stack
- React 18 + TypeScript
- Vite (dev server and build)
- Tailwind CSS
- @hello-pangea/dnd (drag and drop)
- Chart.js + react-chartjs-2 (analytics)
- date-fns (dates, calendar)
- lucide-react (icons)

> Note: Supabase SDK is included in dependencies to enable easy backend integration later, but this build ships with mock data only (no live API calls yet).

---

## Getting Started

### Prerequisites
- Node.js 18+ and npm

### Install & Run
```bash
npm install
npm run dev
```
Then open the printed URL (typically `http://localhost:5173`).

### Build & Preview
```bash
npm run build
npm run preview
```

### Lint
```bash
npm run lint
```

---

## Project Structure
```
src/
  components/
    AnalyticsDashboard.tsx   # Charts and insights
    CalendarView.tsx         # Monthly calendar with due dates
    KanbanBoard.tsx          # DnD board, create task modal
    Layout.tsx               # Shell: sidebar, header, content
    Login.tsx                # Demo login screen
    TaskCard.tsx             # Task details modal, edit, comments
    TaskList.tsx             # Search/filter/sort list view
  contexts/
    AppContext.tsx           # Tasks, projects, comments, activity, behavior
    AuthContext.tsx          # Demo auth + localStorage session
  data/
    staticData.ts            # Mock data (users, projects, tasks, etc.)
  types/
    index.ts                 # Domain models (Task, Project, etc.)
  App.tsx                    # Providers + view switch
  main.tsx                   # App bootstrap (Vite)
```

---

## How It Works (Current Build)
- This is a frontend‑only SPA for fast demos. Data is loaded from `src/data/staticData.ts`.
- `AuthContext` implements a simple credential check against mock users and persists the signed‑in user to `localStorage`.
- `AppContext` holds tasks/projects/comments/activity/behavioral events, exposes actions (`updateTask`, `createTask`, `addComment`, `addActivityLog`, `trackBehavior`) and computes productivity metrics used by Analytics.
- Interactions anywhere (Kanban, List, Task modal) update the same source of truth, so all views stay in sync.

---

## Feature Tour

### 1) Login & Projects
- Demo users are provided; login persists across refresh via `localStorage`.
- Sidebar shows your projects with color badges; switching projects updates all views.

### 2) Kanban Board
- Drag tasks across columns; status updates instantly and activity is logged.
- Create tasks directly into a column; edit details in a modal; add comments.

### 3) Task List
- Search by text; filter by status/priority/assignee; sort by due date/priority/status/created/updated.

### 4) Calendar
- Monthly grid highlights tasks on their due dates with priority and status cues.
- Click a day to see its tasks in a side panel; navigate months easily.

### 5) Analytics
- Charts: weekly completions (line), status distribution (doughnut), time by project (bar).
- Behavioral insights: average session time, most active hour, total sessions.
- Simple recommendations based on your current data.

---

## Backend Story (Planned Integration)

This build does not call a live backend. It’s designed to plug into Supabase (or any API) with minimal changes:

1. Create tables: `users`, `projects`, `project_members`, `tasks`, `comments`, `activity_logs`, `behavioral_data` (plus Storage for files if needed).
2. Add a `supabaseClient.ts` with URL and anon key from env vars.
3. Replace static reads/writes in `AppContext` with Supabase CRUD; use optimistic updates for snappy UX.
4. Subscribe to Supabase Realtime to sync Kanban moves, edits, and comments across users.
5. Optionally move auth to Supabase Auth and set `user` from the session.

Environment variables you’ll likely use:
```bash
VITE_SUPABASE_URL=...
VITE_SUPABASE_ANON_KEY=...
```

---

## Demo Script (Optional, 5–7 minutes)
1. Login with a demo user; pick a project.
2. Kanban: drag a task, create a new task, open modal, edit fields, add a comment.
3. Task List: search, filter, sort.
4. Calendar: navigate months, click a day to see due tasks.
5. Analytics: walk through charts and recommendations.
6. Tech note: React+TS, Context state, Tailwind UI, date‑fns dates, Chart.js charts; ready for Supabase.

---

## Troubleshooting
- Calendar shows no tasks:
  - Ensure a project with tasks is selected in the sidebar.
  - Navigate to the month containing task due dates (or edit a task due date to this month and recheck).

---

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you’d like to change. Keep code type‑safe, follow existing patterns, and include concise commit messages.

---

## License
This project is provided for educational/demo purposes. Add your preferred license if you plan to distribute.

# Taskflow
