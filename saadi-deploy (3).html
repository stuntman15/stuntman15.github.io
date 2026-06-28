<!DOCTYPE html>
<!--
  SAADI — standalone build for GitHub Pages.
  No build step needed: React/Babel/Recharts/Lucide load from CDN at runtime.
  Data is saved in this browser's localStorage (private to this device/browser).

  DEPLOY:
  1. Put this file at the root of your repo as `index.html` (or in /docs).
  2. Push to GitHub.
  3. Repo → Settings → Pages → Source: "Deploy from a branch" → pick the
     branch + folder this file is in → Save.
  4. Your site appears at https://<username>.github.io/<repo-name>/

  NOTE: ES module imports are blocked on file:// URLs by browser security —
  test it via the live GitHub Pages URL (or `python3 -m http.server` locally),
  not by double-clicking the file.
-->
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="apple-mobile-web-app-title" content="Saadi" />
<meta name="theme-color" content="#0b0b10" />
<title>Saadi — Workout &amp; Body Tracker</title>
<style>
  html, body { margin: 0; padding: 0; background: #000; }
  #root { min-height: 100dvh; }
</style>
</head>
<body>
<div id="root">
  <div style="min-height:100dvh;display:flex;align-items:center;justify-content:center;color:#8a8a93;font-family:-apple-system,sans-serif;font-size:14px;">Loading Saadi…</div>
</div>

<script>
  window.addEventListener("error", function (e) {
    showFatalError((e.message || "Unknown error") + (e.filename ? " — " + e.filename.split("/").pop() + ":" + e.lineno : ""));
  });
  window.addEventListener("unhandledrejection", function (e) {
    var reason = e.reason;
    showFatalError("Unhandled promise rejection: " + (reason && reason.message ? reason.message : String(reason)));
  });
  function showFatalError(msg) {
    if (window.__saadiMounted) return;
    var root = document.getElementById("root");
    if (!root) return;
    root.innerHTML =
      '<div style="min-height:100dvh;background:#0b0b10;color:#fff;font-family:-apple-system,sans-serif;padding:28px;box-sizing:border-box;">' +
      '<h2 style="color:#ff7a45;margin:0 0 10px;">Saadi failed to load</h2>' +
      '<p style="color:#cfcfd6;font-size:14px;line-height:1.5;">' + msg.replace(/</g, "&lt;") + "</p>" +
      '<p style="color:#73737d;font-size:12px;margin-top:16px;">Check your internet connection and refresh. If it keeps happening, copy this message and send it back.</p>' +
      "</div>";
  }
</script>
<script type="importmap">
{
  "imports": {
    "react": "https://esm.sh/react@18.3.1",
    "react/jsx-runtime": "https://esm.sh/react@18.3.1/jsx-runtime",
    "react/jsx-dev-runtime": "https://esm.sh/react@18.3.1/jsx-dev-runtime",
    "react-dom": "https://esm.sh/react-dom@18.3.1",
    "react-dom/client": "https://esm.sh/react-dom@18.3.1/client",
    "lucide-react": "https://esm.sh/lucide-react@0.383.0?external=react",
    "recharts": "https://esm.sh/recharts@2.12.7?external=react,react-dom"
  }
}
</script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js" crossorigin="anonymous"></script>

<script type="text/babel" data-type="module" data-presets="react">
import * as React from "react";
import { useState, useEffect, useRef, useMemo } from "react";
import { createRoot } from "react-dom/client";
import {
  Dumbbell, Calendar, Scale, TrendingUp, Plus, X, Check, Play, Pause,
  RotateCcw, ChevronLeft, ChevronRight, Clock, Trash2, Settings, Flame,
  Target, Pencil
} from "lucide-react";
import {
  ResponsiveContainer, LineChart, Line, XAxis, YAxis, CartesianGrid,
  Tooltip, ReferenceLine
} from "recharts";

const STORAGE_KEY = "saadi-app-data";
const WEEKDAYS = ["S", "M", "T", "W", "T", "F", "S"];
const MONTHS = ["January","February","March","April","May","June","July","August","September","October","November","December"];

const pad2 = (n) => String(n).padStart(2, "0");
const toDateStr = (d) => `${d.getFullYear()}-${pad2(d.getMonth() + 1)}-${pad2(d.getDate())}`;
const todayStr = () => toDateStr(new Date());
const parseDateStr = (s) => { const [y, m, d] = s.split("-").map(Number); return new Date(y, m - 1, d); };
const fmtShort = (s) => parseDateStr(s).toLocaleDateString("en-US", { month: "short", day: "numeric" });
const fmtLong = (s) => parseDateStr(s).toLocaleDateString("en-US", { weekday: "short", month: "short", day: "numeric" });
const epley1RM = (w, r) => (!w || !r) ? 0 : (r <= 1 ? Math.round(w) : Math.round(w * (1 + r / 30)));
const uid = () => Date.now().toString(36) + Math.random().toString(36).slice(2, 7);

function fmtElapsed(totalSec) {
  totalSec = Math.max(0, Math.floor(totalSec));
  const h = Math.floor(totalSec / 3600);
  const m = Math.floor((totalSec % 3600) / 60);
  const s = totalSec % 60;
  if (h > 0) return `${h}:${pad2(m)}:${pad2(s)}`;
  return `${m}:${pad2(s)}`;
}

function playBeeps() {
  try {
    const Ctx = window.AudioContext || window.webkitAudioContext;
    const ctx = new Ctx();
    [0, 0.5, 1].forEach((t) => {
      const o = ctx.createOscillator();
      const g = ctx.createGain();
      o.connect(g); g.connect(ctx.destination);
      o.frequency.value = 880;
      o.type = "sine";
      g.gain.setValueAtTime(0.0001, ctx.currentTime + t);
      g.gain.exponentialRampToValueAtTime(0.35, ctx.currentTime + t + 0.01);
      g.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + t + 0.35);
      o.start(ctx.currentTime + t);
      o.stop(ctx.currentTime + t + 0.4);
    });
  } catch (e) {}
}

function defaultData() {
  return {
    workouts: [],
    templates: [],
    bodyweight: [],
    exerciseDefaults: {},
    exerciseTargets: {},
    settings: { targetWeight: null }
  };
}

const SEED_TEMPLATES = [
  { id: "seed-chest-shoulders-tri", name: "Chest + Shoulders + Triceps", exercises: [
    { name: "Bench Press", target: "4x5-8" },
    { name: "Incline Dumbbell Press", target: "3x8-10" },
    { name: "Cable Fly", target: "3x12-15" },
    { name: "Seated Dumbbell Shoulder Press", target: "3x8-10" },
    { name: "Cable Lateral Raises", target: "4x12-20" },
    { name: "Overhead Cable Extension", target: "4x10-15" },
    { name: "Close-Grip Bench Press or Weighted Dips", target: "3x6-10" },
    { name: "Rope Pushdowns", target: "3x12-15" }
  ]},
  { id: "seed-back-biceps", name: "Back + Biceps", exercises: [
    { name: "Pull-Ups or Lat Pulldowns", target: "4x8-12" },
    { name: "Chest-Supported Row", target: "4x8-10" },
    { name: "Single-Arm Cable Row", target: "3x10-12" },
    { name: "Straight-Arm Pulldown", target: "3x12-15" },
    { name: "EZ Bar Curl", target: "4x8-10" },
    { name: "Incline Dumbbell Curl", target: "3x10-12" },
    { name: "Hammer Curl", target: "3x10-12" },
    { name: "Reverse Pec Deck", target: "3x15-20" }
  ]},
  { id: "seed-arms-heavy", name: "Arms (Heavy)", exercises: [
    { name: "Close-Grip Bench Press", target: "4x6-8" },
    { name: "Skull Crushers", target: "4x8-10" },
    { name: "Overhead Cable Extension", target: "3x10-12" },
    { name: "EZ Bar Curl", target: "4x8-10" },
    { name: "Incline Dumbbell Curl", target: "3x10-12" },
    { name: "Hammer Curl", target: "3x10-12" }
  ]},
  { id: "seed-legs", name: "Legs", exercises: [
    { name: "45° Leg Press", target: "4x10-15" },
    { name: "Romanian Deadlift", target: "4x8-10" },
    { name: "Bulgarian Split Squat", target: "3x10 each leg" },
    { name: "Leg Curl", target: "3x10-15" },
    { name: "Leg Extension", target: "3x12-15" },
    { name: "Standing or Seated Calf Raises", target: "4x12-20" }
  ]},
  { id: "seed-arms-shoulders-core", name: "Arms + Shoulders + Core", exercises: [
    { name: "Rope Pushdowns", target: "4x12-15" },
    { name: "Single-Arm Cable Overhead Extension", target: "3x12-15" },
    { name: "Preacher Curl", target: "4x10-12" },
    { name: "Bayesian Cable Curl", target: "3x10-12" },
    { name: "Cable Lateral Raises", target: "5x15-20" },
    { name: "Rear Delt Fly", target: "4x15-20" },
    { name: "Hanging Leg Raises", target: "3x10-15" },
    { name: "Cable Crunches", target: "3x12-15" },
    { name: "Plank", target: "3x45-60 sec" }
  ]}
];

function applySeedTemplates(d) {
  if (d.settings && d.settings.templatesSeededV1) return d;
  const existingIds = new Set(d.templates.map((t) => t.id));
  const toAdd = SEED_TEMPLATES.filter((t) => !existingIds.has(t.id));
  return {
    ...d,
    templates: [...d.templates, ...toAdd],
    settings: { ...d.settings, templatesSeededV1: true }
  };
}

const CSS = `
.app-page{ min-height:100dvh; background:#000; display:flex; justify-content:center;
  font-family:-apple-system,BlinkMacSystemFont,"SF Pro Display","Segoe UI",Roboto,sans-serif; }
.app-root{ width:100%; max-width:430px; min-height:100dvh; background:#0b0b10; color:#f2f2f5;
  display:flex; flex-direction:column; position:relative; overflow:hidden; }
.loading-screen{ align-items:center; justify-content:center; gap:10px; }
.logo-mark{ width:52px; height:52px; border-radius:16px; background:linear-gradient(135deg,#ff8a3d,#ff3b5c);
  display:flex; align-items:center; justify-content:center; margin-bottom:6px; flex-shrink:0; }
.logo-mark.small{ width:26px; height:26px; border-radius:8px; margin:0 8px 0 0; }
.loading-title{ font-size:26px; font-weight:800; letter-spacing:2px; }
.loading-sub{ color:#8a8a93; font-size:13px; }
.topbar{ display:flex; align-items:center; justify-content:space-between;
  padding:calc(16px + env(safe-area-inset-top)) 18px 8px; }
.brand{ display:flex; align-items:center; font-weight:800; font-size:18px; letter-spacing:1px; }
.scroll-area{ flex:1; overflow-y:auto; padding:6px 16px 112px; -webkit-overflow-scrolling:touch; }
.tab-title{ font-size:24px; font-weight:800; margin:6px 0 14px; }
.bottom-nav{ position:absolute; bottom:0; left:0; right:0; display:flex; background:rgba(18,18,24,0.92);
  backdrop-filter:blur(14px); border-top:1px solid #20202a; padding:8px 4px calc(10px + env(safe-area-inset-bottom)); }
.nav-btn{ flex:1; display:flex; flex-direction:column; align-items:center; gap:3px; background:none;
  border:none; color:#74747f; padding:6px 0; font-size:11px; font-weight:600; }
.nav-btn.active{ color:#ff7a45; }
.fab-timer{ position:absolute; right:16px; bottom:84px; z-index:5; width:54px; height:54px; border-radius:50%;
  background:linear-gradient(135deg,#ff8a3d,#ff3b5c); border:none; color:#fff; display:flex; align-items:center;
  justify-content:center; box-shadow:0 6px 18px rgba(255,80,50,0.35); font-size:12px; font-weight:700; }
.fab-timer.active{ width:auto; padding:0 14px; border-radius:27px; }
.card{ background:#15151b; border:1px solid #212129; border-radius:16px; padding:14px; margin-bottom:12px; }
.stat-row{ display:flex; gap:10px; }
.stat-box{ flex:1; background:#15151b; border:1px solid #212129; border-radius:14px; padding:12px 6px; text-align:center; }
.stat-num{ font-size:18px; font-weight:800; }
.streak-val{ display:inline-flex; align-items:center; gap:3px; }
.stat-label{ font-size:10.5px; color:#85858f; margin-top:3px; text-transform:uppercase; letter-spacing:0.4px; }
.btn-primary{ background:linear-gradient(90deg,#ff7a45,#ff3b5c); color:#fff; border:none; border-radius:14px;
  font-weight:700; font-size:15px; padding:13px 18px; display:flex; align-items:center; justify-content:center; gap:6px; }
.btn-primary.full{ width:100%; }
.btn-primary.big{ padding:16px; font-size:16px; }
.btn-primary.small{ padding:10px 13px; border-radius:12px; }
.btn-primary.tiny{ padding:7px 12px; font-size:13px; border-radius:10px; }
.btn-primary.round{ width:56px; height:56px; border-radius:50%; padding:0; }
.btn-ghost{ background:#1c1c24; border:1px solid #2a2a35; color:#f2f2f5; border-radius:12px; padding:11px;
  font-weight:600; font-size:13.5px; display:flex; align-items:center; justify-content:center; gap:6px; width:100%; }
.btn-ghost.full{ margin-top:6px; }
.btn-ghost.danger{ color:#ff6b6b; border-color:#3a2228; background:#1c1418; }
.link-btn{ background:none; border:none; color:#ff7a45; font-weight:600; font-size:13px; }
.link-btn.danger{ color:#ff6b6b; }
.link-btn.danger.confirm{ text-decoration:underline; }
.icon-btn{ background:none; border:none; color:#cfcfd6; padding:4px; display:flex; cursor:pointer; }
.icon-btn.ghost{ color:#85858f; }
.icon-btn-lg{ background:#1c1c24; border:1px solid #2a2a35; border-radius:50%; width:46px; height:46px;
  display:flex; align-items:center; justify-content:center; color:#cfcfd6; }
.section-row{ display:flex; align-items:center; justify-content:space-between; margin:4px 0 8px; }
.section-title{ font-size:14px; font-weight:700; color:#cfcfd6; text-transform:uppercase; letter-spacing:0.5px; }
.empty-hint{ color:#73737d; font-size:13px; padding:8px 2px 16px; }
.template-scroll{ display:flex; gap:10px; overflow-x:auto; padding-bottom:6px; }
.template-chip{ flex:0 0 auto; min-width:168px; background:#15151b; border:1px solid #212129; border-radius:14px; padding:12px; }
.template-chip-name{ font-weight:700; font-size:14px; }
.template-chip-sub{ font-size:11.5px; color:#85858f; margin:3px 0 10px; }
.template-chip-actions{ display:flex; align-items:center; gap:6px; }
.history-card{ display:flex; align-items:center; justify-content:space-between; cursor:pointer; }
.hc-name{ font-weight:700; font-size:14.5px; }
.hc-date{ font-size:12px; color:#85858f; margin-top:2px; }
.hc-meta{ display:flex; gap:10px; font-size:12px; color:#9a9aa5; align-items:center; }
.active-head{ display:flex; align-items:center; justify-content:space-between; margin-bottom:12px; gap:10px; }
.workout-name-input{ background:none; border:none; color:#f2f2f5; font-size:21px; font-weight:800; padding:0; flex:1; min-width:0; }
.ex-card-head{ display:flex; align-items:flex-start; justify-content:space-between; margin-bottom:8px; }
.ex-name{ font-weight:700; font-size:15px; }
.ex-target{ font-size:11.5px; color:#ff8a5a; margin-top:2px; }
.set-row{ display:flex; align-items:center; gap:6px; padding:6px 0; border-top:1px solid #1d1d25; }
.set-row:first-of-type{ border-top:none; }
.set-idx{ width:18px; color:#73737d; font-size:12px; font-weight:700; }
.set-input{ width:54px; background:#1c1c24; border:1px solid #2a2a35; border-radius:9px; color:#f2f2f5;
  padding:7px 6px; font-size:14px; text-align:center; }
.set-unit{ font-size:11px; color:#73737d; }
.set-x{ color:#73737d; }
.set-display{ font-size:13px; color:#cfcfd6; padding:3px 0; }
.add-ex-row{ display:flex; gap:8px; }
.text-input{ width:100%; background:#1c1c24; border:1px solid #2a2a35; border-radius:11px; color:#f2f2f5;
  padding:11px 12px; font-size:14px; }
.text-input.small{ width:64px; flex:none; }
.text-input.target{ width:96px; flex:none; }
.text-input.date{ flex:none; width:130px; }
.field-label{ font-size:12px; font-weight:700; color:#9a9aa5; text-transform:uppercase; letter-spacing:0.4px;
  margin-bottom:7px; display:flex; align-items:center; gap:5px; }
.field-label-row{ display:flex; align-items:center; justify-content:space-between; margin-bottom:4px; }
.log-weight-row{ display:flex; gap:8px; }
.big-stat{ font-size:22px; font-weight:800; }
.template-row{ display:flex; gap:6px; margin-bottom:8px; align-items:center; }
.sheet-backdrop{ position:absolute; inset:0; background:rgba(0,0,0,0.55); z-index:20; display:flex;
  align-items:flex-end; animation:fadeIn .15s ease-out; }
.sheet-panel{ width:100%; max-height:82%; background:#13131a; border-radius:22px 22px 0 0; border:1px solid #232330;
  padding:10px 18px 24px; overflow-y:auto; animation:slideUp .22s ease-out; }
.sheet-grip{ width:36px; height:4px; background:#33333d; border-radius:3px; margin:4px auto 10px; }
.sheet-head{ display:flex; align-items:center; justify-content:space-between; font-weight:800; font-size:16px; margin-bottom:12px; }
.sheet-subtitle{ font-size:13px; color:#9a9aa5; margin-bottom:10px; font-weight:600; }
@keyframes slideUp{ from{ transform:translateY(30px); opacity:0; } to{ transform:translateY(0); opacity:1; } }
@keyframes fadeIn{ from{ opacity:0; } to{ opacity:1; } }
.cal-nav{ display:flex; align-items:center; justify-content:space-between; margin-bottom:8px; }
.cal-month-label{ font-weight:700; font-size:15px; }
.cal-weekdays{ display:grid; grid-template-columns:repeat(7,1fr); text-align:center; color:#73737d; font-size:11px; margin-bottom:4px; }
.cal-grid{ display:grid; grid-template-columns:repeat(7,1fr); gap:4px; }
.cal-cell{ position:relative; aspect-ratio:1; background:none; border:none; border-radius:10px; display:flex;
  flex-direction:column; align-items:center; justify-content:center; color:#e4e4e8; font-size:13px; cursor:pointer; }
.cal-cell.empty{ visibility:hidden; }
.cal-cell.today{ border:1.5px solid #ff7a45; }
.cal-cell.selected{ background:#1c1c24; }
.cal-check{ color:#ff7a45; margin-top:1px; }
.cal-daynum{ line-height:1; }
.chip-scroll{ display:flex; gap:8px; overflow-x:auto; padding-bottom:4px; }
.chip{ flex:0 0 auto; background:#1c1c24; border:1px solid #2a2a35; color:#cfcfd6; border-radius:20px;
  padding:8px 14px; font-size:13px; font-weight:600; }
.chip.active{ background:linear-gradient(90deg,#ff7a45,#ff3b5c); color:#fff; border:none; }
.legend-row{ display:flex; gap:16px; margin-top:6px; font-size:12px; color:#9a9aa5; }
.legend-row .dot{ display:inline-block; width:8px; height:8px; border-radius:50%; margin-right:5px; }
.legend-row .dot.orange{ background:#ff7a45; }
.legend-row .dot.blue{ background:#5b8cff; }
.timer-wrap{ display:flex; flex-direction:column; align-items:center; padding:8px 0; }
.timer-circle{ width:180px; height:180px; border-radius:50%; display:flex; align-items:center; justify-content:center; margin-bottom:18px; }
.timer-circle-inner{ width:152px; height:152px; border-radius:50%; background:#13131a; display:flex;
  align-items:center; justify-content:center; font-size:34px; font-weight:800; }
.timer-adjust-row{ display:flex; gap:10px; margin-bottom:18px; }
.timer-controls{ display:flex; align-items:center; gap:18px; }
.settings-info{ color:#9a9aa5; font-size:13.5px; line-height:1.6; margin-bottom:18px; }
.settings-info strong{ color:#f2f2f5; }
input[type="date"]{ color-scheme: dark; }
::-webkit-scrollbar{ width:0; height:0; }
button{ cursor:pointer; }
`;

function Sheet({ open, onClose, title, children }) {
  if (!open) return null;
  return (
    <div className="sheet-backdrop" onClick={onClose}>
      <div className="sheet-panel" onClick={(e) => e.stopPropagation()}>
        <div className="sheet-grip" />
        <div className="sheet-head">
          <span>{title}</span>
          <button className="icon-btn" onClick={onClose}><X size={18} /></button>
        </div>
        <div className="sheet-body">{children}</div>
      </div>
    </div>
  );
}

function StatBox({ label, value, accent }) {
  return (
    <div className="stat-box">
      <div className="stat-num" style={accent ? { color: "#ff7a45" } : undefined}>{value}</div>
      <div className="stat-label">{label}</div>
    </div>
  );
}

function TemplateEditor({ initial, onSave }) {
  const [name, setName] = useState(initial ? initial.name : "");
  const [rows, setRows] = useState(
    initial && initial.exercises && initial.exercises.length
      ? initial.exercises.map((e) => ({ name: e.name, target: e.target || "" }))
      : [{ name: "", target: "" }]
  );

  function updateRow(i, field, val) {
    setRows((r) => r.map((row, idx) => (idx !== i ? row : { ...row, [field]: val })));
  }
  function addRow() { setRows((r) => [...r, { name: "", target: "" }]); }
  function removeRow(i) { setRows((r) => r.filter((_, idx) => idx !== i)); }
  function save() {
    const exercises = rows
      .filter((r) => r.name.trim())
      .map((r) => ({ name: r.name.trim(), target: r.target.trim() }));
    if (!name.trim() || exercises.length === 0) return;
    onSave({ id: initial ? initial.id : uid(), name: name.trim(), exercises });
  }

  return (
    <div>
      <span className="field-label">Template name</span>
      <input className="text-input" placeholder="e.g. Push Day" value={name} onChange={(e) => setName(e.target.value)} />
      <span className="field-label" style={{ marginTop: 16 }}>Exercises</span>
      {rows.map((row, i) => (
        <div className="template-row" key={i}>
          <input className="text-input" placeholder="Exercise name" value={row.name} onChange={(e) => updateRow(i, "name", e.target.value)} />
          <input className="text-input target" placeholder="4x8-10" value={row.target} onChange={(e) => updateRow(i, "target", e.target.value)} />
          <button className="icon-btn ghost" onClick={() => removeRow(i)}><X size={16} /></button>
        </div>
      ))}
      <button className="btn-ghost" onClick={addRow}><Plus size={16} /> Add exercise</button>
      <button className="btn-primary full" style={{ marginTop: 20 }} onClick={save}>Save Template</button>
    </div>
  );
}

function WorkoutTab({ data, setData, activeWorkout, setActiveWorkout, startRest }) {
  const [historySheet, setHistorySheet] = useState(null);
  const [showTemplateEditor, setShowTemplateEditor] = useState(false);
  const [editingTemplate, setEditingTemplate] = useState(null);
  const [exerciseInput, setExerciseInput] = useState("");
  const [confirmDiscard, setConfirmDiscard] = useState(false);

  const exerciseHistoryNames = useMemo(() => {
    const s = new Set(Object.keys(data.exerciseDefaults));
    data.workouts.forEach((w) => w.exercises.forEach((e) => s.add(e.name)));
    return Array.from(s).sort();
  }, [data]);

  function startBlank() {
    setActiveWorkout({ id: uid(), date: todayStr(), name: "Workout", startedAt: Date.now(), exercises: [] });
  }
  function startFromTemplate(t) {
    setActiveWorkout({
      id: uid(), date: todayStr(), name: t.name, startedAt: Date.now(),
      exercises: t.exercises.map((e) => ({ id: uid(), name: e.name, target: e.target, sets: [] }))
    });
  }
  function addExercise() {
    if (!exerciseInput.trim()) return;
    setActiveWorkout((w) => ({ ...w, exercises: [...w.exercises, { id: uid(), name: exerciseInput.trim(), sets: [] }] }));
    setExerciseInput("");
  }
  function removeExercise(exId) {
    setActiveWorkout((w) => ({ ...w, exercises: w.exercises.filter((e) => e.id !== exId) }));
  }
  function addSet(exId) {
    setActiveWorkout((w) => {
      const exercises = w.exercises.map((ex) => {
        if (ex.id !== exId) return ex;
        const prev = ex.sets[ex.sets.length - 1];
        const def = data.exerciseDefaults[ex.name];
        const weight = prev ? prev.weight : (def ? def.weight : 0);
        const reps = prev ? prev.reps : (def ? def.reps : 0);
        return { ...ex, sets: [...ex.sets, { weight, reps }] };
      });
      return { ...w, exercises };
    });
    startRest();
  }
  function updateSet(exId, idx, field, val) {
    setActiveWorkout((w) => ({
      ...w,
      exercises: w.exercises.map((ex) => (ex.id !== exId ? ex : {
        ...ex, sets: ex.sets.map((s, i) => (i !== idx ? s : { ...s, [field]: val === "" ? "" : Number(val) }))
      }))
    }));
  }
  function removeSet(exId, idx) {
    setActiveWorkout((w) => ({
      ...w,
      exercises: w.exercises.map((ex) => (ex.id !== exId ? ex : { ...ex, sets: ex.sets.filter((_, i) => i !== idx) }))
    }));
  }
  function finishWorkout() {
    const cleaned = activeWorkout.exercises
      .filter((e) => e.sets.length > 0)
      .map((e) => ({ ...e, sets: e.sets.map((s) => ({ weight: Number(s.weight) || 0, reps: Number(s.reps) || 0 })) }));
    if (cleaned.length === 0) { setActiveWorkout(null); return; }
    const finished = {
      ...activeWorkout, exercises: cleaned,
      durationMin: Math.max(1, Math.round((Date.now() - activeWorkout.startedAt) / 60000))
    };
    const newDefaults = { ...data.exerciseDefaults };
    cleaned.forEach((ex) => {
      const last = ex.sets[ex.sets.length - 1];
      if (last) newDefaults[ex.name] = { weight: last.weight, reps: last.reps };
    });
    setData((d) => ({ ...d, workouts: [finished, ...d.workouts], exerciseDefaults: newDefaults }));
    setActiveWorkout(null);
  }
  function deleteWorkout(id) {
    setData((d) => ({ ...d, workouts: d.workouts.filter((w) => w.id !== id) }));
    setHistorySheet(null);
  }
  function deleteTemplate(id) {
    setData((d) => ({ ...d, templates: d.templates.filter((t) => t.id !== id) }));
  }
  function openNewTemplate() { setEditingTemplate(null); setShowTemplateEditor(true); }
  function openEditTemplate(t) { setEditingTemplate(t); setShowTemplateEditor(true); }
  function saveTemplate(t) {
    setData((d) => {
      const exists = d.templates.some((x) => x.id === t.id);
      const templates = exists ? d.templates.map((x) => (x.id === t.id ? t : x)) : [...d.templates, t];
      return { ...d, templates };
    });
    setShowTemplateEditor(false);
    setEditingTemplate(null);
  }

  const weekAgo = new Date(); weekAgo.setDate(weekAgo.getDate() - 6);
  const weekAgoStr = toDateStr(weekAgo);
  const thisWeek = data.workouts.filter((w) => w.date >= weekAgoStr).length;
  const total = data.workouts.length;
  const workoutDateSet = useMemo(() => new Set(data.workouts.map((w) => w.date)), [data.workouts]);
  let streak = 0;
  {
    let cur = new Date();
    let cs = todayStr();
    if (!workoutDateSet.has(cs)) { cur.setDate(cur.getDate() - 1); cs = toDateStr(cur); }
    while (workoutDateSet.has(cs)) { streak++; cur.setDate(cur.getDate() - 1); cs = toDateStr(cur); }
  }

  if (activeWorkout) {
    const elapsedSec = Math.floor((Date.now() - activeWorkout.startedAt) / 1000);
    const totalSets = activeWorkout.exercises.reduce((a, e) => a + e.sets.length, 0);
    return (
      <div>
        <div className="active-head">
          <input className="workout-name-input" value={activeWorkout.name}
            onChange={(e) => setActiveWorkout((w) => ({ ...w, name: e.target.value }))} />
          {!confirmDiscard ? (
            <button className="link-btn danger" onClick={() => { setConfirmDiscard(true); setTimeout(() => setConfirmDiscard(false), 3000); }}>Discard</button>
          ) : (
            <button className="link-btn danger confirm" onClick={() => setActiveWorkout(null)}>Tap to confirm</button>
          )}
        </div>
        <div className="stat-row">
          <StatBox label="Exercises" value={activeWorkout.exercises.length} />
          <StatBox label="Elapsed" value={fmtElapsed(elapsedSec)} accent />
          <StatBox label="Total Sets" value={totalSets} />
        </div>

        {activeWorkout.exercises.map((ex) => (
          <div className="card" key={ex.id}>
            <div className="ex-card-head">
              <div>
                <div className="ex-name">{ex.name}</div>
                {ex.target && <div className="ex-target">Target: {ex.target}</div>}
              </div>
              <button className="icon-btn" onClick={() => removeExercise(ex.id)}><X size={16} /></button>
            </div>
            {ex.sets.map((s, i) => (
              <div className="set-row" key={i}>
                <span className="set-idx">{i + 1}</span>
                <input type="number" inputMode="decimal" className="set-input" value={s.weight}
                  onChange={(e) => updateSet(ex.id, i, "weight", e.target.value)} />
                <span className="set-unit">lbs</span>
                <span className="set-x">×</span>
                <input type="number" inputMode="numeric" className="set-input" value={s.reps}
                  onChange={(e) => updateSet(ex.id, i, "reps", e.target.value)} />
                <span className="set-unit">reps</span>
                <button className="icon-btn ghost" onClick={() => removeSet(ex.id, i)}><Trash2 size={14} /></button>
              </div>
            ))}
            <button className="btn-ghost full" onClick={() => addSet(ex.id)}><Plus size={15} /> Add Set</button>
          </div>
        ))}

        <div className="card">
          <div className="add-ex-row">
            <input className="text-input" list="ex-names" placeholder="Add exercise (e.g. Barbell Row)"
              value={exerciseInput} onChange={(e) => setExerciseInput(e.target.value)}
              onKeyDown={(e) => { if (e.key === "Enter") addExercise(); }} />
            <datalist id="ex-names">
              {exerciseHistoryNames.map((n) => <option value={n} key={n} />)}
            </datalist>
            <button className="btn-primary small" onClick={addExercise}><Plus size={16} /></button>
          </div>
        </div>

        <button className="btn-primary full" style={{ marginTop: 8 }} onClick={finishWorkout}>Finish Workout</button>
      </div>
    );
  }

  return (
    <div>
      <h1 className="tab-title">Workouts</h1>
      <button className="btn-primary full big" onClick={startBlank}>Start Workout</button>

      <div className="stat-row" style={{ marginTop: 14 }}>
        <StatBox label="This Week" value={thisWeek} />
        <StatBox label="Streak" value={<span className="streak-val"><Flame size={13} />{streak}</span>} accent />
        <StatBox label="Total" value={total} />
      </div>

      <div className="section-row" style={{ marginTop: 18 }}>
        <span className="section-title">Templates</span>
        <button className="link-btn" onClick={openNewTemplate}>+ New</button>
      </div>
      {data.templates.length === 0 ? (
        <div className="empty-hint">No templates yet — build one to quick-start a routine.</div>
      ) : (
        <div className="template-scroll">
          {data.templates.map((t) => (
            <div className="template-chip" key={t.id}>
              <div className="template-chip-name">{t.name}</div>
              <div className="template-chip-sub">{t.exercises.length} exercises</div>
              <div className="template-chip-actions">
                <button className="btn-primary tiny" onClick={() => startFromTemplate(t)}>Start</button>
                <button className="icon-btn ghost" onClick={() => openEditTemplate(t)}><Pencil size={13} /></button>
                <button className="icon-btn ghost" onClick={() => deleteTemplate(t.id)}><Trash2 size={13} /></button>
              </div>
            </div>
          ))}
        </div>
      )}

      <div className="section-row" style={{ marginTop: 18 }}>
        <span className="section-title">Recent Workouts</span>
      </div>
      {data.workouts.length === 0 ? (
        <div className="empty-hint">Your workout history will show up here.</div>
      ) : data.workouts.slice(0, 30).map((w) => (
        <div className="card history-card" key={w.id} onClick={() => setHistorySheet(w)}>
          <div>
            <div className="hc-name">{w.name}</div>
            <div className="hc-date">{fmtLong(w.date)}</div>
          </div>
          <div className="hc-meta">
            <span>{w.exercises.length} ex</span>
            <span>{w.exercises.reduce((a, e) => a + e.sets.length, 0)} sets</span>
            {w.durationMin && <span>{w.durationMin} min</span>}
          </div>
        </div>
      ))}

      <Sheet open={!!historySheet} onClose={() => setHistorySheet(null)} title={historySheet ? fmtLong(historySheet.date) : ""}>
        {historySheet && (
          <div>
            <div className="sheet-subtitle">{historySheet.name}</div>
            {historySheet.exercises.map((ex) => (
              <div className="card" key={ex.id}>
                <div className="ex-name">{ex.name}</div>
                {ex.sets.map((s, i) => (
                  <div className="set-display" key={i}>Set {i + 1} — {s.weight} lbs × {s.reps}</div>
                ))}
              </div>
            ))}
            <button className="btn-ghost full danger" onClick={() => deleteWorkout(historySheet.id)}>
              <Trash2 size={15} /> Delete Workout
            </button>
          </div>
        )}
      </Sheet>

      <Sheet open={showTemplateEditor} onClose={() => { setShowTemplateEditor(false); setEditingTemplate(null); }}
        title={editingTemplate ? "Edit Template" : "New Template"}>
        <TemplateEditor initial={editingTemplate} onSave={saveTemplate} />
      </Sheet>
    </div>
  );
}

function CalendarTab({ data }) {
  const [view, setView] = useState(() => { const d = new Date(); return { y: d.getFullYear(), m: d.getMonth() }; });
  const [selectedDay, setSelectedDay] = useState(null);

  const workoutsByDate = useMemo(() => {
    const map = {};
    data.workouts.forEach((w) => { (map[w.date] = map[w.date] || []).push(w); });
    return map;
  }, [data.workouts]);

  const firstDay = new Date(view.y, view.m, 1);
  const startWeekday = firstDay.getDay();
  const daysInMonth = new Date(view.y, view.m + 1, 0).getDate();
  const cells = [];
  for (let i = 0; i < startWeekday; i++) cells.push(null);
  for (let d = 1; d <= daysInMonth; d++) cells.push(d);

  function prevMonth() { setView((v) => (v.m === 0 ? { y: v.y - 1, m: 11 } : { y: v.y, m: v.m - 1 })); }
  function nextMonth() { setView((v) => (v.m === 11 ? { y: v.y + 1, m: 0 } : { y: v.y, m: v.m + 1 })); }
  function goToday() { const d = new Date(); setView({ y: d.getFullYear(), m: d.getMonth() }); setSelectedDay(todayStr()); }

  const today = todayStr();
  const selectedWorkouts = selectedDay ? (workoutsByDate[selectedDay] || []) : [];

  return (
    <div>
      <h1 className="tab-title">Calendar</h1>
      <div className="card">
        <div className="cal-nav">
          <button className="icon-btn" onClick={prevMonth}><ChevronLeft size={20} /></button>
          <span className="cal-month-label">{MONTHS[view.m]} {view.y}</span>
          <button className="icon-btn" onClick={nextMonth}><ChevronRight size={20} /></button>
        </div>
        <div className="cal-weekdays">
          {WEEKDAYS.map((w, i) => <span key={i}>{w}</span>)}
        </div>
        <div className="cal-grid">
          {cells.map((d, i) => {
            if (d === null) return <div className="cal-cell empty" key={i} />;
            const ds = `${view.y}-${pad2(view.m + 1)}-${pad2(d)}`;
            const has = !!workoutsByDate[ds];
            const isToday = ds === today;
            const isSelected = ds === selectedDay;
            return (
              <button key={i}
                className={`cal-cell ${isToday ? "today" : ""} ${isSelected ? "selected" : ""}`}
                onClick={() => setSelectedDay(ds)}>
                <span className="cal-daynum">{d}</span>
                {has && <Check size={11} className="cal-check" />}
              </button>
            );
          })}
        </div>
        <button className="link-btn" style={{ marginTop: 8 }} onClick={goToday}>Jump to Today</button>
      </div>

      {selectedDay && (
        <div className="card">
          <div className="sheet-subtitle">{fmtLong(selectedDay)}</div>
          {selectedWorkouts.length === 0 ? (
            <div className="empty-hint">No workout logged this day.</div>
          ) : selectedWorkouts.map((w) => (
            <div key={w.id} style={{ marginTop: 8 }}>
              <div className="ex-name">{w.name}</div>
              {w.exercises.map((ex) => (
                <div className="set-display" key={ex.id}>{ex.name} — {ex.sets.length} sets</div>
              ))}
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

function BodyTab({ data, setData }) {
  const [weightInput, setWeightInput] = useState("");
  const [dateInput, setDateInput] = useState(todayStr());
  const [editingTarget, setEditingTarget] = useState(false);
  const [targetInput, setTargetInput] = useState(data.settings.targetWeight ?? "");

  const sorted = useMemo(() => [...data.bodyweight].sort((a, b) => a.date.localeCompare(b.date)), [data.bodyweight]);
  const last = sorted.length ? sorted[sorted.length - 1].weight : null;
  const target = data.settings.targetWeight;

  function logWeight() {
    const w = parseFloat(weightInput);
    if (!w || w <= 0 || !dateInput) return;
    setData((d) => {
      const idx = d.bodyweight.findIndex((b) => b.date === dateInput);
      let bw;
      if (idx >= 0) { bw = [...d.bodyweight]; bw[idx] = { date: dateInput, weight: w }; }
      else bw = [...d.bodyweight, { date: dateInput, weight: w }];
      return { ...d, bodyweight: bw };
    });
    setWeightInput("");
  }
  function deleteEntry(date) {
    setData((d) => ({ ...d, bodyweight: d.bodyweight.filter((b) => b.date !== date) }));
  }
  function saveTarget() {
    const v = parseFloat(targetInput);
    setData((d) => ({ ...d, settings: { ...d.settings, targetWeight: v > 0 ? v : null } }));
    setEditingTarget(false);
  }

  const chartData = sorted.map((b) => ({ ...b, label: fmtShort(b.date) }));

  return (
    <div>
      <h1 className="tab-title">Body Weight</h1>
      <div className="stat-row">
        <StatBox label="Last" value={last ? `${last} lbs` : "—"} accent />
        <StatBox label="Target" value={target ? `${target} lbs` : "Not set"} />
        <StatBox label="Logs" value={sorted.length} />
      </div>

      <div className="card">
        <span className="field-label">Log Weight</span>
        <div className="log-weight-row">
          <input className="text-input" type="number" inputMode="decimal" placeholder="lbs"
            value={weightInput} onChange={(e) => setWeightInput(e.target.value)} />
          <input className="text-input date" type="date" value={dateInput} max={todayStr()}
            onChange={(e) => setDateInput(e.target.value)} />
          <button className="btn-primary small" onClick={logWeight}><Plus size={16} /></button>
        </div>
      </div>

      {sorted.length >= 2 && (
        <div className="card">
          <span className="field-label">Trend</span>
          <ResponsiveContainer width="100%" height={200}>
            <LineChart data={chartData} margin={{ top: 10, right: 10, left: -20, bottom: 0 }}>
              <CartesianGrid stroke="#232330" strokeDasharray="3 3" vertical={false} />
              <XAxis dataKey="label" stroke="#7a7a85" fontSize={11} tickLine={false} axisLine={false} />
              <YAxis stroke="#7a7a85" fontSize={11} tickLine={false} axisLine={false} width={40} />
              <Tooltip contentStyle={{ background: "#1c1c24", border: "1px solid #2a2a35", borderRadius: 10, fontSize: 12 }}
                labelStyle={{ color: "#f2f2f5" }} itemStyle={{ color: "#ff7a45" }} />
              {target && <ReferenceLine y={target} stroke="#5a5a65" strokeDasharray="4 4" />}
              <Line type="monotone" dataKey="weight" stroke="#ff7a45" strokeWidth={3} dot={{ r: 3, fill: "#ff7a45" }} activeDot={{ r: 5 }} />
            </LineChart>
          </ResponsiveContainer>
        </div>
      )}

      <div className="card">
        <div className="field-label-row">
          <span className="field-label"><Target size={12} /> Target Weight</span>
          {!editingTarget && <button className="icon-btn ghost" onClick={() => { setEditingTarget(true); setTargetInput(target ?? ""); }}><Pencil size={14} /></button>}
        </div>
        {editingTarget ? (
          <div className="log-weight-row">
            <input className="text-input" type="number" value={targetInput} onChange={(e) => setTargetInput(e.target.value)} />
            <button className="btn-primary small" onClick={saveTarget}><Check size={16} /></button>
          </div>
        ) : (
          <div className="big-stat">{target ? `${target} lbs` : "Not set"}</div>
        )}
      </div>

      <div className="section-row" style={{ marginTop: 10 }}><span className="section-title">History</span></div>
      {sorted.length === 0 ? (
        <div className="empty-hint">Log your first weigh-in above.</div>
      ) : [...sorted].reverse().map((b) => (
        <div className="history-card card" key={b.date}>
          <span>{fmtLong(b.date)}</span>
          <div className="hc-meta">
            <span>{b.weight} lbs</span>
            <button className="icon-btn ghost" onClick={() => deleteEntry(b.date)}><Trash2 size={14} /></button>
          </div>
        </div>
      ))}
    </div>
  );
}

function StatsTab({ data, setData }) {
  const exerciseNames = useMemo(() => {
    const s = new Set();
    data.workouts.forEach((w) => w.exercises.forEach((e) => { if (e.sets.length) s.add(e.name); }));
    return Array.from(s).sort();
  }, [data.workouts]);

  const [selected, setSelected] = useState(exerciseNames[0] || "");
  useEffect(() => { if (!selected && exerciseNames.length) setSelected(exerciseNames[0]); }, [exerciseNames, selected]);

  const [editingTarget, setEditingTarget] = useState(false);
  const [targetInput, setTargetInput] = useState("");

  const series = useMemo(() => {
    if (!selected) return [];
    const pts = [];
    data.workouts.forEach((w) => {
      const ex = w.exercises.find((e) => e.name === selected);
      if (!ex || !ex.sets.length) return;
      let maxW = 0, best1 = 0;
      ex.sets.forEach((s) => {
        if (s.weight > maxW) maxW = s.weight;
        const e1 = epley1RM(s.weight, s.reps);
        if (e1 > best1) best1 = e1;
      });
      pts.push({ date: w.date, label: fmtShort(w.date), maxWeight: maxW, est1rm: best1 });
    });
    return pts.sort((a, b) => a.date.localeCompare(b.date));
  }, [data.workouts, selected]);

  const bestEver1rm = series.length ? Math.max(...series.map((p) => p.est1rm)) : 0;
  const bestEverMax = series.length ? Math.max(...series.map((p) => p.maxWeight)) : 0;
  const target = data.exerciseTargets[selected];

  function saveTarget() {
    const v = parseFloat(targetInput);
    setData((d) => ({ ...d, exerciseTargets: { ...d.exerciseTargets, [selected]: v > 0 ? v : undefined } }));
    setEditingTarget(false);
  }

  return (
    <div>
      <h1 className="tab-title">Exercise Stats</h1>
      {exerciseNames.length === 0 ? (
        <div className="empty-hint">Log a workout to see progress charts here.</div>
      ) : (
        <>
          <div className="chip-scroll">
            {exerciseNames.map((n) => (
              <button key={n} className={`chip ${n === selected ? "active" : ""}`} onClick={() => setSelected(n)}>{n}</button>
            ))}
          </div>

          <div className="stat-row" style={{ marginTop: 12 }}>
            <StatBox label="Est. 1RM" value={`${bestEver1rm} lbs`} accent />
            <StatBox label="Max Weight" value={`${bestEverMax} lbs`} />
          </div>

          <div className="card">
            <span className="field-label">{selected} — Trend</span>
            <ResponsiveContainer width="100%" height={200}>
              <LineChart data={series} margin={{ top: 10, right: 10, left: -20, bottom: 0 }}>
                <CartesianGrid stroke="#232330" strokeDasharray="3 3" vertical={false} />
                <XAxis dataKey="label" stroke="#7a7a85" fontSize={11} tickLine={false} axisLine={false} />
                <YAxis stroke="#7a7a85" fontSize={11} tickLine={false} axisLine={false} width={40} />
                <Tooltip contentStyle={{ background: "#1c1c24", border: "1px solid #2a2a35", borderRadius: 10, fontSize: 12 }}
                  labelStyle={{ color: "#f2f2f5" }} />
                {target && <ReferenceLine y={target} stroke="#5a5a65" strokeDasharray="4 4" />}
                <Line type="monotone" dataKey="maxWeight" stroke="#ff7a45" strokeWidth={3} dot={{ r: 3, fill: "#ff7a45" }} />
                <Line type="monotone" dataKey="est1rm" stroke="#5b8cff" strokeWidth={2} strokeDasharray="4 3" dot={false} />
              </LineChart>
            </ResponsiveContainer>
            <div className="legend-row">
              <span><i className="dot orange" /> Max Weight</span>
              <span><i className="dot blue" /> Est. 1RM</span>
            </div>
          </div>

          <div className="card">
            <div className="field-label-row">
              <span className="field-label"><Target size={12} /> Target Max Weight</span>
              {!editingTarget && <button className="icon-btn ghost" onClick={() => { setEditingTarget(true); setTargetInput(target ?? ""); }}><Pencil size={14} /></button>}
            </div>
            {editingTarget ? (
              <div className="log-weight-row">
                <input className="text-input" type="number" value={targetInput} onChange={(e) => setTargetInput(e.target.value)} />
                <button className="btn-primary small" onClick={saveTarget}><Check size={16} /></button>
              </div>
            ) : (
              <div className="big-stat">{target ? `${target} lbs` : "Not set"}</div>
            )}
          </div>
        </>
      )}
    </div>
  );
}

function RestTimerContent({ duration, remaining, running, onAdjust, onToggle, onReset }) {
  const pct = Math.max(0, Math.min(1, remaining / duration));
  return (
    <div className="timer-wrap">
      <div className="timer-circle" style={{ background: `conic-gradient(#ff7a45 ${pct * 360}deg, #232330 0deg)` }}>
        <div className="timer-circle-inner">{fmtElapsed(remaining)}</div>
      </div>
      <div className="timer-adjust-row">
        <button className="chip" onClick={() => onAdjust(-15)}>−15s</button>
        <button className="chip" onClick={() => onAdjust(15)}>+15s</button>
      </div>
      <div className="timer-controls">
        <button className="icon-btn-lg" onClick={onReset}><RotateCcw size={20} /></button>
        <button className="btn-primary round" onClick={onToggle}>{running ? <Pause size={22} /> : <Play size={22} />}</button>
      </div>
    </div>
  );
}

function FloatingTimerButton({ remaining, duration, running, onClick }) {
  const active = running || remaining !== duration;
  return (
    <button className={`fab-timer ${active ? "active" : ""}`} onClick={onClick}>
      {active ? <span>{fmtElapsed(remaining)}</span> : <Clock size={22} />}
    </button>
  );
}

function SettingsContent({ onReset }) {
  const [confirm, setConfirm] = useState(false);
  return (
    <div>
      <div className="settings-info">
        <p>Saadi stores your workouts, templates, and body weight logs in this browser's local storage.</p>
        <p>Units: <strong>lbs</strong></p>
      </div>
      {!confirm ? (
        <button className="btn-ghost full danger" onClick={() => { setConfirm(true); setTimeout(() => setConfirm(false), 4000); }}>
          <Trash2 size={15} /> Reset All Data
        </button>
      ) : (
        <button className="btn-primary full" style={{ background: "#d9314a" }} onClick={onReset}>
          Tap again to confirm reset
        </button>
      )}
    </div>
  );
}

function Saadi() {
  const [data, setData] = useState(null);
  const [loaded, setLoaded] = useState(false);
  const [tab, setTab] = useState("workout");
  const [activeWorkout, setActiveWorkout] = useState(null);
  const [, setTick] = useState(0);
  const [settingsOpen, setSettingsOpen] = useState(false);
  const [timerSheetOpen, setTimerSheetOpen] = useState(false);

  const [restDuration, setRestDuration] = useState(90);
  const [restRemaining, setRestRemaining] = useState(90);
  const [restRunning, setRestRunning] = useState(false);
  const restRef = useRef(null);
  const saveRef = useRef(null);

  useEffect(() => {
    try {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (raw) {
        const parsed = JSON.parse(raw);
        let merged = {
          ...defaultData(), ...parsed,
          exerciseDefaults: parsed.exerciseDefaults || {},
          exerciseTargets: parsed.exerciseTargets || {},
          settings: { ...defaultData().settings, ...(parsed.settings || {}) }
        };
        merged = applySeedTemplates(merged);
        setData(merged);
      } else {
        setData(applySeedTemplates(defaultData()));
      }
    } catch (e) {
      setData(applySeedTemplates(defaultData()));
    } finally {
      setLoaded(true);
    }
  }, []);

  useEffect(() => {
    if (!loaded || !data) return;
    if (saveRef.current) clearTimeout(saveRef.current);
    saveRef.current = setTimeout(() => {
      try { localStorage.setItem(STORAGE_KEY, JSON.stringify(data)); } catch (e) {}
    }, 400);
    return () => { if (saveRef.current) clearTimeout(saveRef.current); };
  }, [data, loaded]);

  useEffect(() => {
    if (!activeWorkout) return;
    const id = setInterval(() => setTick((t) => t + 1), 1000);
    return () => clearInterval(id);
  }, [activeWorkout]);

  useEffect(() => {
    if (restRunning) {
      restRef.current = setInterval(() => {
        setRestRemaining((r) => {
          if (r <= 1) { setRestRunning(false); playBeeps(); return 0; }
          return r - 1;
        });
      }, 1000);
    }
    return () => clearInterval(restRef.current);
  }, [restRunning]);

  function startRest() { setRestRemaining(restDuration); setRestRunning(true); }
  function toggleRest() { if (restRemaining === 0) setRestRemaining(restDuration); setRestRunning((r) => !r); }
  function resetRest() { setRestRunning(false); setRestRemaining(restDuration); }
  function adjustRest(delta) {
    setRestDuration((d) => {
      const nd = Math.max(15, d + delta);
      setRestRemaining(nd);
      setRestRunning(false);
      return nd;
    });
  }
  function resetAllData() {
    try { localStorage.removeItem(STORAGE_KEY); } catch (e) {}
    setData(defaultData());
    setActiveWorkout(null);
    setSettingsOpen(false);
  }

  if (!loaded || !data) {
    return (
      <div className="app-page">
        <style>{CSS}</style>
        <div className="app-root loading-screen">
          <div className="logo-mark"><Dumbbell size={26} color="#fff" /></div>
          <div className="loading-title">SAADI</div>
          <div className="loading-sub">Track. Measure. Progress.</div>
        </div>
      </div>
    );
  }

  const TABS = [
    { key: "workout", label: "Workout", icon: Dumbbell },
    { key: "calendar", label: "Calendar", icon: Calendar },
    { key: "body", label: "Body", icon: Scale },
    { key: "stats", label: "Stats", icon: TrendingUp }
  ];

  return (
    <div className="app-page">
      <style>{CSS}</style>
      <div className="app-root">
        <div className="topbar">
          <div className="brand">
            <div className="logo-mark small"><Dumbbell size={15} color="#fff" /></div>
            SAADI
          </div>
          <button className="icon-btn" onClick={() => setSettingsOpen(true)}><Settings size={20} /></button>
        </div>

        <div className="scroll-area">
          {tab === "workout" && <WorkoutTab data={data} setData={setData} activeWorkout={activeWorkout} setActiveWorkout={setActiveWorkout} startRest={startRest} />}
          {tab === "calendar" && <CalendarTab data={data} />}
          {tab === "body" && <BodyTab data={data} setData={setData} />}
          {tab === "stats" && <StatsTab data={data} setData={setData} />}
        </div>

        <FloatingTimerButton remaining={restRemaining} duration={restDuration} running={restRunning} onClick={() => setTimerSheetOpen(true)} />

        <div className="bottom-nav">
          {TABS.map((t) => {
            const Icon = t.icon;
            return (
              <button key={t.key} className={`nav-btn ${tab === t.key ? "active" : ""}`} onClick={() => setTab(t.key)}>
                <Icon size={21} />
                <span>{t.label}</span>
              </button>
            );
          })}
        </div>

        <Sheet open={timerSheetOpen} onClose={() => setTimerSheetOpen(false)} title="Rest Timer">
          <RestTimerContent duration={restDuration} remaining={restRemaining} running={restRunning}
            onAdjust={adjustRest} onToggle={toggleRest} onReset={resetRest} />
        </Sheet>

        <Sheet open={settingsOpen} onClose={() => setSettingsOpen(false)} title="Settings">
          <SettingsContent onReset={resetAllData} />
        </Sheet>
      </div>
    </div>
  );
}

try {
  const root = createRoot(document.getElementById("root"));
  root.render(<Saadi />);
  window.__saadiMounted = true;
} catch (err) {
  window.showFatalError ? window.showFatalError(String(err && err.message ? err.message : err)) : console.error(err);
}
</script>
</body>
</html>
