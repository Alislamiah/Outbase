<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#07111f">
<title>Outbase — Build your project</title>
<link rel="icon" href="icon.png">

<style>
*{box-sizing:border-box}
body{
 margin:0;
 background:radial-gradient(circle at 50% 0%,#102b50 0,#07111f 48%,#040914 100%);
 color:#fff;font-family:Arial,sans-serif;min-height:100vh
}
header{
 height:70px;padding:0 7%;display:flex;align-items:center;
 justify-content:space-between;border-bottom:1px solid #ffffff12;
 background:#07111fbb;position:sticky;top:0;z-index:20
}
.brand{font-size:24px;font-weight:800;letter-spacing:.5px}
.brand span{color:#38a4ff}
header a{color:#b9cce2;text-decoration:none;font-size:14px}

main{max-width:1000px;margin:65px auto;padding:25px;text-align:center}
.tag{
 display:inline-block;padding:9px 15px;border:1px solid #245b8d;
 border-radius:30px;color:#69baff;background:#0b2340;font-size:12px
}
h1{font-size:clamp(35px,7vw,58px);margin:24px 0 15px;line-height:1.12}
h1 span{color:#45aaff}
.sub{color:#9fb2c9;line-height:1.8;max-width:570px;margin:0 auto 35px}
.panel{
 max-width:560px;margin:35px auto 0;padding:30px;
 background:linear-gradient(145deg,#10243b,#0a1729);
 border:1px solid #203c5d;border-radius:20px;text-align:left;
 box-shadow:0 20px 65px #0005
}
.panel h2{margin:0 0 10px;font-size:21px}
.panel p{color:#91a9c2;font-size:13px;line-height:1.7}
input{
 width:100%;padding:16px;background:#071321;border:1px solid #29415d;
 border-radius:10px;color:#fff;font-size:15px;outline:none;margin:13px 0
}
input:focus{border-color:#36a4ff}
button{font-family:Arial,sans-serif}
.primary{
 border:0;border-radius:10px;padding:15px 22px;
 background:linear-gradient(100deg,#1675d1,#35aaff);
 color:white;font-weight:bold;font-size:15px;cursor:pointer;width:100%
}
.primary:disabled{opacity:.5;cursor:wait}
.message{font-size:13px;color:#ffb1b1;min-height:20px;margin-top:12px}

.projects-section{
 max-width:850px;margin:48px auto 0;text-align:left
}
.section-title{
 display:flex;justify-content:space-between;align-items:center;
 gap:12px;margin-bottom:18px
}
.section-title h2{font-size:21px}
.section-title small{color:#8ca7c1}
.project-list{
 display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:13px
}
.project-card{
 background:linear-gradient(145deg,#10243b,#0a1729);
 border:1px solid #203c5d;border-radius:13px;
 padding:18px;min-width:0
}
.project-card strong{display:block;font-size:15px;overflow-wrap:anywhere}
.project-card small{display:block;color:#8da8c2;margin-top:9px;overflow-wrap:anywhere}
.project-card a{
 display:inline-block;margin-top:15px;color:#50b3ff;
 text-decoration:none;font-size:13px
}
.empty{
 padding:25px;border:1px dashed #29445d;border-radius:12px;
 color:#91a9c2;text-align:center;font-size:13px;line-height:1.8
}

#loading{
 position:fixed;inset:0;background:#07111f;z-index:100;
 display:flex;align-items:center;justify-content:center;
 color:#53adff;font-weight:bold
}
.spinner{
 width:30px;height:30px;border:3px solid #ffffff20;
 border-top-color:#38a4ff;border-radius:50%;
 animation:spin .8s linear infinite;margin:auto auto 15px
}
@keyframes spin{to{transform:rotate(360deg)}}

nav{
 position:fixed;bottom:0;left:0;right:0;
 background:#07111ff2;border-top:1px solid #ffffff15;
 display:flex;justify-content:center;gap:35px;padding:15px;z-index:15
}
nav a{color:#a8bdd3;text-decoration:none;font-size:13px}
nav a.active{color:#49aaff}
</style>
</head>

<body>

<div id="loading">
 <div style="text-align:center">
  <div class="spinner"></div>
  Loading Outbase...
 </div>
</div>

<div id="app" style="visibility:hidden">

<header>
 <div class="brand">Out<span>base</span></div>
 <a href="Projects.html" id="accountLink">My account</a>
</header>

<main>
 <div class="tag">YOUR PROJECT. YOUR CONTROL.</div>
 <h1>Build your next<br><span>great project.</span></h1>
 <p class="sub">Create and manage your application projects locally and instantly with Outbase.</p>

 <section class="panel">
  <h2>Start a new project</h2>
  <p>Create a project workspace and receive its unique Project ID.</p>

  <div id="createArea" style="display:none">
   <input id="projectName" maxlength="45" placeholder="Enter your project name">
   <button class="primary" id="createBtn">Create Project</button>
  </div>

  <button class="primary" id="startBtn">Start Project</button>
  <div class="message" id="message"></div>
 </section>

 <section class="projects-section">
  <div class="section-title">
   <h2>Your projects</h2>
   <small id="projectCount">0 projects</small>
  </div>
  <div class="project-list" id="allProjects">
   <div class="empty">Loading projects...</div>
  </div>
 </section>
</main>

<nav>
 <a class="active" href="index.html">Home</a>
 <a href="https://alislamiah.github.io/Gemalot/">Gemalot</a>
 <a href="https://alislamiah.github.io/outhub/">Outhub</a>
</nav>

</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";
import { getAuth, onAuthStateChanged, setPersistence, browserLocalPersistence } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-auth.js";

const firebaseConfig = {
 apiKey: "AIzaSyBrv1ky0Br5nLb68uvdXE3o6QdzTKpIU4g",
 authDomain: "alislamiah-ai-34202.firebaseapp.com",
 projectId: "alislamiah-ai-34202",
 storageBucket: "alislamiah-ai-34202.firebasestorage.app",
 messagingSenderId: "683051452829",
 appId: "1:683051452829:web:e96e40422c7f31e563c774",
 measurementId: "G-LFQLND010S"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);

let currentUser = null;
let allUserProjects = [];
const LOGIN_URL = "signin.html";

const startBtn = document.getElementById("startBtn");
const createArea = document.getElementById("createArea");
const createBtn = document.getElementById("createBtn");
const nameInput = document.getElementById("projectName");
const message = document.getElementById("message");

function getStorageKey(){
 return "outbase_projects_" + (currentUser ? currentUser.uid : "guest");
}

function makeProjectId(name){
 const clean = name.trim().replace(/[^a-zA-Z0-9_-]+/g, "-").replace(/^-+|-+$/g, "");
 const digits = Math.floor(1000 + Math.random() * 99999996);
 return clean + "-" + digits;
}

function loadProjects(){
 try {
  allUserProjects = JSON.parse(localStorage.getItem(getStorageKey()) || "[]");
  allUserProjects.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
  renderProjects();
 } catch(e){
  allUserProjects = [];
  renderProjects();
 }
}

function renderProjects(){
 const all = document.getElementById("allProjects");
 document.getElementById("projectCount").textContent = allUserProjects.length + " projects";

 if(allUserProjects.length){
  all.innerHTML = allUserProjects.map(p => `
   <div class="project-card">
    <strong>${escapeHTML(p.name)}</strong>
    <small>ID: ${escapeHTML(p.id)}</small>
    <a href="Projects.html">Manage project →</a>
   </div>
  `).join("");
 } else {
  all.innerHTML = '<div class="empty">You have no projects yet. Start your first project!</div>';
 }
}

function escapeHTML(str){
 return String(str ?? "").replace(/[&<>"']/g, c => ({
  "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;"
 }[c]));
}

startBtn.onclick = () => {
 if(!currentUser){
  location.href = `${LOGIN_URL}?redirect=${encodeURIComponent(window.location.href)}`;
  return;
 }
 createArea.style.display = "block";
 startBtn.style.display = "none";
 nameInput.focus();
};

createBtn.onclick = () => {
 if(!currentUser) return;
 const name = nameInput.value.trim();
 if(name.length < 2){
  message.textContent = "Please enter a project name.";
  return;
 }

 createBtn.disabled = true;
 message.style.color = "#91a9c2";
 message.textContent = "Creating project locally...";

 try {
  const projects = JSON.parse(localStorage.getItem(getStorageKey()) || "[]");
  
  const newProject = {
   id: makeProjectId(name),
   name: name,
   ownerUid: currentUser.uid,
   createdAt: Date.now(),
   apiKey: "ob_" + crypto.randomUUID().replace(/-/g, "")
  };

  projects.unshift(newProject);
  localStorage.setItem(getStorageKey(), JSON.stringify(projects));

  message.style.color = "#4ade80";
  message.textContent = "Project created successfully!";
  
  setTimeout(() => {
   loadProjects();
   nameInput.value = "";
   createArea.style.display = "none";
   startBtn.style.display = "block";
   createBtn.disabled = false;
  }, 500);

 } catch(error) {
  message.style.color = "#ff7777";
  message.textContent = "Error: " + error.message;
  createBtn.disabled = false;
 }
};

nameInput.addEventListener("keydown", e => {
 if(e.key === "Enter") createBtn.click();
});

await setPersistence(auth, browserLocalPersistence);

onAuthStateChanged(auth, (user) => {
 if(!user){
  location.href = `${LOGIN_URL}?redirect=${encodeURIComponent(window.location.href)}`;
  return;
 }
 currentUser = user;
 document.getElementById("accountLink").textContent = user.displayName || user.email || "My account";

 loadProjects();
 document.getElementById("loading").style.display = "none";
 document.getElementById("app").style.visibility = "visible";
});
</script>

</body>
</html>
