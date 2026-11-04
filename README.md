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
body{margin:0;background:radial-gradient(circle at 50% 0%,#102b50 0,#07111f 48%,#040914 100%);color:#fff;font-family:Arial,sans-serif;min-height:100vh}
header{height:70px;padding:0 7%;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #ffffff12;background:#07111fbb}
.brand{font-size:24px;font-weight:800;letter-spacing:.5px;color:#fff}
.brand span{color:#38a4ff}
header a{color:#b9cce2;text-decoration:none;font-size:14px}
main{max-width:900px;margin:75px auto;padding:25px;text-align:center}
.tag{display:inline-block;padding:9px 15px;border:1px solid #245b8d;border-radius:30px;color:#69baff;background:#0b2340;font-size:12px}
h1{font-size:clamp(35px,7vw,58px);margin:24px 0 15px;line-height:1.12}
h1 span{color:#45aaff}
.sub{color:#9fb2c9;line-height:1.8;max-width:570px;margin:0 auto 35px}
.panel{max-width:560px;margin:35px auto 0;padding:30px;background:linear-gradient(145deg,#10243b,#0a1729);border:1px solid #203c5d;border-radius:20px;text-align:left;box-shadow:0 20px 65px #0005}
.panel h2{margin:0 0 10px;font-size:21px}
.panel p{color:#91a9c2;font-size:13px;line-height:1.7}
input{width:100%;padding:16px;background:#071321;border:1px solid #29415d;border-radius:10px;color:#fff;font-size:15px;outline:none;margin:13px 0}
input:focus{border-color:#36a4ff}
button{border:0;border-radius:10px;padding:15px 22px;background:linear-gradient(100deg,#1675d1,#35aaff);color:white;font-weight:bold;font-size:15px;cursor:pointer;width:100%}
button:disabled{opacity:.5;cursor:wait}
.message{font-size:13px;color:#ffb1b1;min-height:20px;margin-top:12px}
.features{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-top:55px;text-align:left}
.feature{padding:20px;background:#0c1b2d;border:1px solid #1b3450;border-radius:14px}
.feature b{display:block;margin-bottom:9px}
.feature small{color:#91a9c2;line-height:1.6}
nav{position:fixed;bottom:0;left:0;right:0;background:#07111ff2;border-top:1px solid #ffffff15;display:flex;justify-content:center;gap:35px;padding:15px}
nav a{color:#a8bdd3;text-decoration:none;font-size:13px}
nav a.active{color:#49aaff}
@media(max-width:600px){main{margin:45px auto;padding:17px}.panel{padding:22px}.features{grid-template-columns:1fr;gap:10px}header{padding:0 18px}nav{gap:22px}}
</style>
</head>
<body>
<header>
  <div class="brand">Out<span>base</span></div>
  <a href="signin.html" id="accountLink">Sign in</a>
</header>

<main>
  <div class="tag">YOUR PROJECT. YOUR CONTROL.</div>
  <h1>Build your next<br><span>great project.</span></h1>
  <p class="sub">Create and manage your application projects with Outbase. Start building your project from one simple dashboard.</p>

  <section class="panel">
    <h2>Start a new project</h2>
    <p>Create a project workspace and receive its unique Project ID.</p>
    <div id="createArea" style="display:none">
      <input id="projectName" maxlength="45" placeholder="Enter your project name">
      <button id="createBtn">Create Project</button>
    </div>
    <button id="startBtn">Start Project</button>
    <div class="message" id="message"></div>
  </section>

  <div class="features">
    <div class="feature"><b>Project Management</b><small>Keep your project information organized in one place.</small></div>
    <div class="feature"><b>Authentication</b><small>Configure authentication options for your application.</small></div>
    <div class="feature"><b>Developer Tools</b><small>Access your project settings and integration details.</small></div>
  </div>
</main>

<nav>
  <a class="active" href="index.html">Home</a>
  <a href="https://alislamiah.github.io/Gemalot/">Gemalot</a>
  <a href="https://alislamiah.github.io/outhub/">Outhub</a>
</nav>

<script type="module">
import {initializeApp} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";
import {getAuth,onAuthStateChanged} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-auth.js";

const firebaseConfig={
 apiKey:"AIzaSyBrv1ky0Br5nLb68uvdXE3o6QdzTKpIU4g",
 authDomain:"alislamiah-ai-34202.firebaseapp.com",
 projectId:"alislamiah-ai-34202",
 storageBucket:"alislamiah-ai-34202.firebasestorage.app",
 messagingSenderId:"683051452829",
 appId:"1:683051452829:web:e96e40422c7f31e563c774",
 measurementId:"G-LFQLND010S"
};

const app=initializeApp(firebaseConfig);
const auth=getAuth(app);
let currentUser=null;

const startBtn=document.getElementById("startBtn");
const createArea=document.getElementById("createArea");
const createBtn=document.getElementById("createBtn");
const nameInput=document.getElementById("projectName");
const message=document.getElementById("message");

onAuthStateChanged(auth,user=>{
 currentUser=user;
 document.getElementById("accountLink").textContent=user?(user.displayName||user.email||"My account"):"Sign in";
});

startBtn.onclick=()=>{
 if(!currentUser){
  location.href="signin.html";
  return;
 }
 createArea.style.display="block";
 startBtn.style.display="none";
 nameInput.focus();
};

function makeProjectId(name){
 const clean=name.trim().replace(/[^a-zA-Z0-9_-]+/g,"-").replace(/^-+|-+$/g,"");
 return clean+"-"+Math.floor(100000+Math.random()*900000);
}

createBtn.onclick=()=>{
 if(!currentUser){
  location.href="signin.html";
  return;
 }
 const name=nameInput.value.trim();
 if(name.length<2){
  message.textContent="Please enter a project name (at least 2 characters).";
  return;
 }

 createBtn.disabled=true;
 const key="outbase_projects_"+currentUser.uid;
 let projects=[];
 try{projects=JSON.parse(localStorage.getItem(key)||"[]")}catch(e){projects=[]}

 const project={
  id:makeProjectId(name),
  name:name,
  createdAt:new Date().toISOString(),
  apiKey:"ob_"+crypto.randomUUID().replace(/-/g,""),
  auth:{alislamiah:{enabled:false,domain:""},outhub:{enabled:false,domain:""}},
  users:[]
 };

 projects.unshift(project);
 localStorage.setItem(key,JSON.stringify(projects));
 localStorage.setItem("outbase_active_project_"+currentUser.uid,project.id);
 location.href="Projects.html";
};
</script>
</body>
</html>