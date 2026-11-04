
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
.header-left{display:flex;align-items:center;gap:15px}
.brand{font-size:24px;font-weight:800;letter-spacing:.5px}
.brand span{color:#38a4ff}
header a{color:#b9cce2;text-decoration:none;font-size:14px}
.menu-btn{
 width:42px;height:42px;background:#10243b;border:1px solid #29445f;
 border-radius:10px;display:flex;flex-direction:column;
 align-items:center;justify-content:center;gap:5px;cursor:pointer
}
.menu-btn span{width:19px;height:2px;background:white;border-radius:5px}

/* Sidebar */
.overlay{
 position:fixed;inset:0;background:#0009;z-index:29;display:none
}
.overlay.show{display:block}
.sidebar{
 position:fixed;left:0;top:0;bottom:0;width:270px;max-width:85%;
 background:#09182a;border-right:1px solid #ffffff15;
 z-index:30;padding:23px 17px;
 transform:translateX(-105%);transition:.25s ease
}
.sidebar.open{transform:translateX(0)}
.side-head{
 display:flex;justify-content:space-between;align-items:center;
 padding-bottom:22px;border-bottom:1px solid #ffffff12;margin-bottom:22px
}
.side-title{font-size:21px;font-weight:bold}
.side-title span{color:#38a4ff}
.close-menu{background:none;border:0;color:white;font-size:27px;cursor:pointer}
.side-label{font-size:11px;color:#6f89a5;padding:12px}
.side-btn{
 width:100%;display:flex;align-items:center;gap:13px;
 padding:15px 13px;border:0;border-radius:10px;
 background:transparent;color:#c4d5e8;text-align:left;
 font-size:14px;cursor:pointer;margin:3px 0;text-decoration:none
}
.side-btn:hover{background:#102d4b;color:#55b7ff}
.side-btn span{font-size:19px;width:22px;text-align:center}

/* Main */
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
.features{
 display:grid;grid-template-columns:repeat(3,1fr);
 gap:14px;margin-top:55px;text-align:left
}
.feature{
 padding:20px;background:#0c1b2d;border:1px solid #1b3450;border-radius:14px
}
.feature b{display:block;margin-bottom:9px}
.feature small{color:#91a9c2;line-height:1.6}

/* Projects */
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

/* Upgrade */
.limit-panel{
 display:none;max-width:560px;margin:20px auto 0;padding:24px;
 background:#251d16;border:1px solid #75502a;border-radius:15px;text-align:left
}
.limit-panel h3{color:#ffc477;margin:0 0 10px}
.limit-panel p{font-size:13px;color:#d4b99b;line-height:1.8}
.plan-list{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-top:15px}
.plan{
 background:#101d2c;border:1px solid #35465b;padding:13px;border-radius:10px
}
.plan b{display:block;margin-bottom:6px}
.plan small{color:#9bb0c5}

/* Loading */
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

@media(max-width:600px){
 main{margin:45px auto;padding:17px}
 .panel{padding:22px}
 .features{grid-template-columns:1fr;gap:10px}
 header{padding:0 18px}
 nav{gap:22px}
 .project-list{grid-template-columns:1fr}
 .projects-section{padding:0 17px}
}
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
 <div class="header-left">
  <button class="menu-btn" id="menuBtn" aria-label="Open menu">
   <span></span><span></span><span></span>
  </button>
  <div class="brand">Out<span>base</span></div>
 </div>
 <a href="Projects.html" id="accountLink">My account</a>
</header>

<div class="overlay" id="overlay"></div>

<aside class="sidebar" id="sidebar">
 <div class="side-head">
  <div class="side-title">Out<span>base</span></div>
  <button class="close-menu" id="closeMenu">×</button>
 </div>

 <div class="side-label">DEVELOPER DASHBOARD</div>

 <a class="side-btn" href="Projects.html?view=settings">
  <span>⚙</span> Settings
 </a>

 <a class="side-btn" href="Projects.html?view=authentication">
  <span>🔐</span> Authentication
 </a>

 <div class="side-label">ACCOUNT</div>

 <a class="side-btn" href="Projects.html">
  <span>▦</span> Your projects
 </a>
</aside>

<main>

 <div class="tag">YOUR PROJECT. YOUR CONTROL.</div>

 <h1>Build your next<br><span>great project.</span></h1>

 <p class="sub">
 Create and manage your application projects with Outbase.
 Start building your project from one simple dashboard.
 </p>

 <section class="panel">

  <h2>Start a new project</h2>

  <p>Create a project workspace and receive its unique Project ID.</p>

  <div id="createArea" style="display:none">
   <input id="projectName" maxlength="45"
    placeholder="Enter your project name">

   <button class="primary" id="createBtn">Create Project</button>
  </div>

  <button class="primary" id="startBtn">Start Project</button>

  <div class="message" id="message"></div>

 </section>

 <section class="limit-panel" id="limitPanel">
  <h3>Upgrade To Pro</h3>

  <p>
   You have reached your project creation limit.
   Upgrade your plan to create more projects.
  </p>

  <div class="plan-list">
   <div class="plan">
    <b>Pro</b>
    <small>08 projects per account</small>
   </div>

   <div class="plan">
    <b>Gold</b>
    <small>16 projects per account</small>
   </div>

   <div class="plan">
    <b>Extra</b>
    <small>20 projects per account</small>
   </div>
  </div>
 </section>

 <section class="projects-section">

  <div class="section-title">
   <h2>Your last projects</h2>
   <small id="lastCount">0 projects</small>
  </div>

  <div class="project-list" id="lastProjects">
   <div class="empty">Loading projects...</div>
  </div>

  <div class="section-title" style="margin-top:35px">
   <h2>Your projects</h2>
   <small id="projectCount">0 projects</small>
  </div>

  <div class="project-list" id="allProjects">
   <div class="empty">Loading projects...</div>
  </div>

 </section>

 <div class="features">
  <div class="feature">
   <b>Project Management</b>
   <small>Keep your project information organized in one place.</small>
  </div>

  <div class="feature">
   <b>Authentication</b>
   <small>Configure authentication options for your application.</small>
  </div>

  <div class="feature">
   <b>Developer Tools</b>
   <small>Access your project settings and integration details.</small>
  </div>
 </div>

</main>

<nav>
 <a class="active" href="index.html">Home</a>
 <a href="https://alislamiah.github.io/Gemalot/">Gemalot</a>
 <a href="https://alislamiah.github.io/outhub/">Outhub</a>
</nav>

</div>

<script type="module">

import {
 initializeApp
} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";

import {
 getAuth,
 onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-auth.js";

import {
 getFirestore,
 collection,
 doc,
 getDoc,
 getDocs,
 runTransaction,
 serverTimestamp
} from "https://www.gstatic.com/firebasejs/13.0.0/firebase-firestore.js";


/* FIREBASE CONFIG */

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
const db=getFirestore(app);

let currentUser=null;
let allUserProjects=[];


/* PLAN LIMITS */

const PLAN_LIMITS={
 free:4,
 pro:8,
 gold:16,
 extra:20
};


/* ELEMENTS */

const startBtn=document.getElementById("startBtn");
const createArea=document.getElementById("createArea");
const createBtn=document.getElementById("createBtn");
const nameInput=document.getElementById("projectName");
const message=document.getElementById("message");

const sidebar=document.getElementById("sidebar");
const overlay=document.getElementById("overlay");


/* SIDEBAR */

function openMenu(){
 sidebar.classList.add("open");
 overlay.classList.add("show");
}

function closeMenu(){
 sidebar.classList.remove("open");
 overlay.classList.remove("show");
}

document.getElementById("menuBtn").onclick=openMenu;
document.getElementById("closeMenu").onclick=closeMenu;
overlay.onclick=closeMenu;


/* FIRESTORE PATHS */

function accountRef(uid){
 return doc(db,"users",uid);
}

function projectsRef(uid){
 return collection(db,"users",uid,"projects");
}


/* PROJECT ID */

function makeProjectId(name){
 const clean=name.trim()
  .replace(/[^a-zA-Z0-9_-]+/g,"-")
  .replace(/^-+|-+$/g,"");

 const digits=Math.floor(1000+Math.random()*99999996);

 return clean+"-"+digits;
}


/* DATE FORMAT */

function formatDate(date){
 if(!date)return "Recently created";

 const d=date.toDate?date.toDate():new Date(date);

 return d.toLocaleDateString("en-US",{
  year:"numeric",
  month:"short",
  day:"numeric"
 });
}


/* LOAD PROJECTS */

async function loadProjects(){

 const snapshot=await getDocs(projectsRef(currentUser.uid));

 allUserProjects=snapshot.docs.map(d=>({
  ...d.data(),
  documentId:d.id
 }));

 allUserProjects.sort((a,b)=>{
  const dateA=a.createdAt?.toMillis?.()||0;
  const dateB=b.createdAt?.toMillis?.()||0;
  return dateB-dateA;
 });

 renderProjects();
}


/* RENDER PROJECTS */

function renderProjects(){

 const last=document.getElementById("lastProjects");
 const all=document.getElementById("allProjects");

 document.getElementById("projectCount").textContent=
  allUserProjects.length+" projects";

 const latest=allUserProjects.slice(0,3);

 document.getElementById("lastCount").textContent=
  latest.length+" projects";

 function card(p){
  return `
   <div class="project-card">
    <strong>${escapeHTML(p.name)}</strong>
    <small>Project ID: ${escapeHTML(p.id)}</small>
    <small>Created: ${formatDate(p.createdAt)}</small>
    <a href="Projects.html">Manage project →</a>
   </div>
  `;
 }

 if(latest.length){
  last.innerHTML=latest.map(card).join("");
 }else{
  last.innerHTML='<div class="empty">Your recent projects will appear here.</div>';
 }

 if(allUserProjects.length){
  all.innerHTML=allUserProjects.map(card).join("");
 }else{
  all.innerHTML='<div class="empty">You have no projects yet. Start your first project!</div>';
 }
}


/* HTML SAFETY */

function escapeHTML(value){
 return String(value??"").replace(/[&<>"']/g,c=>({
  "&":"&amp;",
  "<":"&lt;",
  ">":"&gt;",
  '"':"&quot;",
  "'":"&#39;"
 }[c]));
}


/* START PROJECT */

startBtn.onclick=()=>{

 if(!currentUser){
  location.href="signin.html";
  return;
 }

 createArea.style.display="block";
 startBtn.style.display="none";

 nameInput.focus();
};


/* CREATE PROJECT */

createBtn.onclick=async()=>{

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
 message.style.color="#91a9c2";
 message.textContent="Creating your project...";

 try{

  const uid=currentUser.uid;
  const accRef=accountRef(uid);

  // Create a unique Firestore document reference
  const newProjectRef=doc(projectsRef(uid));

  // Project ID includes random digits
  const projectId=makeProjectId(name);

  await runTransaction(db,async(transaction)=>{

   const accountSnap=await transaction.get(accRef);

   let accountData=accountSnap.exists()
    ?accountSnap.data()
    :{};

   const plan=String(accountData.plan||"free").toLowerCase();

   const limit=PLAN_LIMITS[plan]||4;

   let activeProjects=Number(accountData.activeProjects);

   // Initialize the counter for existing accounts
   if(!Number.isFinite(activeProjects)){
    activeProjects=allUserProjects.length;
   }

   const reachedLimits=accountData.reachedLimits||{};

   /*
    IMPORTANT:
    Once the account reaches its plan limit,
    deleting a project does NOT restore that quota.
   */

   if(reachedLimits[plan]===true){
    throw new Error("PROJECT_LIMIT_REACHED");
   }

   if(activeProjects>=limit){

    transaction.set(accRef,{
     activeProjects:activeProjects,
     reachedLimits:{
      ...reachedLimits,
      [plan]:true
     }
    },{merge:true});

    throw new Error("PROJECT_LIMIT_REACHED");
   }

   const nextCount=activeProjects+1;

   const updatedLimits={
    ...reachedLimits
   };

   // Mark the quota as consumed when it is reached
   if(nextCount>=limit){
    updatedLimits[plan]=true;
   }

   transaction.set(accRef,{
    activeProjects:nextCount,
    plan:plan,
    reachedLimits:updatedLimits
   },{merge:true});

   transaction.set(newProjectRef,{
    id:projectId,
    name:name,
    ownerUid:uid,
    createdAt:serverTimestamp(),
    apiKey:"ob_"+crypto.randomUUID().replace(/-/g,""),
    auth:{
     alislamiah:{
      enabled:false,
      domain:""
     },
     outhub:{
      enabled:false,
      domain:""
     }
    },
    users:[]
   });

  });

  message.style.color="#4ade80";
  message.textContent="Project created successfully!";

  setTimeout(()=>{
   location.href="Projects.html";
  },700);

 }catch(error){

  console.error(error);

  if(error.message==="PROJECT_LIMIT_REACHED"){

   document.getElementById("limitPanel").style.display="block";

   message.style.color="#ffc477";
   message.textContent="Project limit reached. Upgrade your plan to continue.";

  }else{

   message.style.color="#ff7777";
   message.textContent="Failed to create project: "+error.message;

  }

  createBtn.disabled=false;
 }

};


/* ENTER KEY */

nameInput.addEventListener("keydown",e=>{
 if(e.key==="Enter")createBtn.click();
});


/* AUTHENTICATION SESSION */

onAuthStateChanged(auth,async(user)=>{

 if(!user){
  location.replace("signin.html");
  return;
 }

 currentUser=user;

 document.getElementById("accountLink").textContent=
  user.displayName||user.email||"My account";

 try{

  await loadProjects();

  document.getElementById("loading").style.display="none";
  document.getElementById("app").style.visibility="visible";

 }catch(error){

  console.error(error);

  document.getElementById("loading").innerHTML=
   '<div style="text-align:center;color:#ff8585">Failed to load projects. Please refresh.</div>';

 }

});

</script>

</body>
</html>
