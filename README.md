from pathlib import Path

html = r'''<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>رحلة النحو | المستوى الأول</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@500;600;700;800;900&family=Changa:wght@600;700;800&display=swap');
:root{
--navy:#17213b;--blue:#4d65d9;--violet:#7866d9;--mint:#62c7ae;--gold:#efbf62;
--paper:#fbfaf7;--ink:#202942;--muted:#788198;--line:#e8e8ee;--danger:#d96773;
}
*{box-sizing:border-box}body{margin:0;background:#eef2f8;color:var(--ink);font-family:Cairo,sans-serif}
button,input,textarea{font:inherit}button{cursor:pointer}
.shell{min-height:100vh;max-width:1280px;margin:auto;background:var(--paper);position:relative;overflow:hidden}
.top{height:76px;display:flex;align-items:center;padding:0 28px;border-bottom:1px solid #e4e6ec;background:#fff;gap:18px}
.mark{display:flex;align-items:center;gap:10px;font-weight:900;font-size:20px}.markIcon{width:42px;height:42px;border-radius:13px;background:var(--navy);display:grid;place-items:center;color:#fff;font-family:Changa;font-size:22px}
.userMini{margin-right:auto;display:flex;align-items:center;gap:9px;color:var(--muted);font-size:13px}.miniAvatar{width:38px;height:38px;border-radius:12px;background:#edf0ff;display:grid;place-items:center}
main{padding:28px}
.page{display:none}.page.active{display:block;animation:fade .35s ease}@keyframes fade{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
/* onboarding */
.welcome{min-height:calc(100vh - 76px);display:grid;grid-template-columns:1.1fr .9fr;gap:25px;align-items:center;padding:45px}
.intro h1{font-family:Changa;font-size:clamp(40px,6vw,76px);line-height:1.05;margin:12px 0;color:var(--navy)}.intro p{font-size:18px;color:var(--muted);max-width:570px;line-height:1.9}
.pill{display:inline-block;background:#e9edff;color:#4e60c7;padding:8px 15px;border-radius:30px;font-weight:800;font-size:13px}
.form{background:#fff;border:1px solid var(--line);border-radius:28px;padding:27px;box-shadow:0 20px 50px #27345112}
label{font-weight:800;display:block;margin-bottom:9px}input{width:100%;padding:15px;border:2px solid var(--line);border-radius:15px;outline:none}input:focus{border-color:var(--blue)}
.genderRow{display:flex;gap:12px;margin:12px 0 20px}.gender{flex:1;border:2px solid var(--line);background:#fff;border-radius:18px;padding:10px}.gender.selected{border-color:var(--blue);background:#f2f4ff}.gender svg{height:105px;width:100%}.gender span{display:block;font-weight:900}
.primary{border:0;background:var(--navy);color:#fff;border-radius:15px;padding:14px 21px;font-weight:900;box-shadow:0 12px 24px #17213b22}.primary:hover{background:#243252}.primary:disabled{opacity:.4;cursor:not-allowed}
/* map */
.mapHead{display:flex;justify-content:space-between;align-items:end;gap:15px;margin-bottom:22px}.mapHead h2{font-family:Changa;font-size:38px;margin:0}.mapHead p{margin:3px 0;color:var(--muted)}
.map{background:#f5f2e9;border:1px solid #e7e2d6;border-radius:30px;min-height:600px;padding:28px;position:relative;overflow:hidden}
.map:before{content:"";position:absolute;inset:0;background:linear-gradient(120deg,transparent 49%,#ded8c8 50%,transparent 51%),linear-gradient(20deg,transparent 49%,#ded8c8 50%,transparent 51%);opacity:.35}
.path{position:absolute;left:9%;right:9%;top:50%;height:5px;background:#d7d0c0;transform:rotate(-2deg);border-radius:99px}
.levels{position:relative;display:grid;grid-template-columns:repeat(4,1fr);gap:25px;align-items:center;min-height:520px}
.level{position:relative;text-align:center}.node{width:86px;height:86px;margin:auto;border-radius:27px;background:#fff;border:5px solid #dfe3eb;box-shadow:0 12px 24px #29354a16;display:grid;place-items:center;font-family:Changa;font-size:22px;font-weight:900;transition:.25s}.level.current .node{border-color:var(--blue);background:#5a6ddd;color:#fff;transform:translateY(-7px);box-shadow:0 17px 28px #5265d955}.level.done .node{border-color:var(--mint);color:#238d77}.level.locked .node{background:#e7e8ec;color:#9298a6}.level:nth-child(odd){transform:translateY(-45px)}.level:nth-child(even){transform:translateY(45px)}.levelName{font-weight:900;margin-top:10px}.levelSub{font-size:11px;color:var(--muted)}.lock{font-size:11px;color:#9298a6;margin-top:4px}
.startLevel{margin-top:20px;display:flex;justify-content:center}
/* game */
.gameHead{display:flex;align-items:center;gap:15px;margin-bottom:16px}.back{border:1px solid var(--line);background:#fff;border-radius:13px;padding:9px 13px;font-weight:800}.gameTitle{flex:1}.gameTitle b{font-size:13px;color:#5362c9}.gameTitle h2{font-family:Changa;margin:2px 0;font-size:28px}.meter{width:250px}.meterTop{display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:5px}.meterBar{height:9px;background:#e9ebf1;border-radius:99px;overflow:hidden}.meterFill{height:100%;width:0;background:linear-gradient(90deg,var(--blue),var(--violet));transition:.35s}
.timer{background:#fff;border:1px solid var(--line);border-radius:13px;padding:10px 14px;font-weight:900}.timer.low{color:var(--danger)}
.gameLayout{display:grid;grid-template-columns:1fr 250px;gap:18px}.board{background:#fff;border:1px solid var(--line);border-radius:28px;padding:30px;min-height:590px;display:flex;flex-direction:column;box-shadow:0 18px 45px #2734510d}.boardTag{color:#5868ce;font-size:12px;font-weight:900}.board h2{font-family:Changa;font-size:33px;margin:7px 0}.boardDesc{color:var(--muted);margin:0 0 20px}.stage{flex:1;display:flex;align-items:center;justify-content:center}
.words{display:flex;flex-wrap:wrap;gap:13px;justify-content:center;max-width:700px}.word{min-width:125px;padding:18px 22px;border:2px solid #e1e5ed;border-radius:18px;background:#fff;font-size:21px;font-weight:900;transition:.2s;box-shadow:0 8px 15px #27345108}.word:hover{transform:translateY(-4px);border-color:#8793e4}.word.chosen{background:#eef0ff;border-color:var(--blue);color:#4354bd}
.choiceGrid{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;width:min(700px,100%)}.choice{background:#fff;border:2px solid #e1e5ed;border-radius:20px;padding:22px;font-weight:900;font-size:19px;transition:.2s}.choice:hover{transform:translateY(-3px);border-color:#8793e4}.choice.good{background:#eaf8f3;border-color:var(--mint)}.choice.bad{background:#fff0f2;border-color:var(--danger)}
.write{width:min(720px,100%)}textarea{width:100%;height:145px;border:2px solid #e1e5ed;border-radius:20px;padding:18px;resize:none;outline:none}.textareaActions{display:flex;justify-content:flex-end;margin-top:10px}
.feedback{min-height:48px;border-radius:15px;padding:11px 14px;background:#f5f6f9;color:var(--muted);font-weight:800;margin-top:18px}.feedback.good{background:#eaf8f3;color:#227a64}.feedback.bad{background:#fff0f2;color:#ad4351}.feedback.hint{background:#fff8e8;color:#946a26}
.nav{display:flex;justify-content:space-between;margin-top:13px}.nav button{border:1px solid var(--line);background:#fff;border-radius:13px;padding:11px 17px;font-weight:800}.nav .next{background:var(--navy);color:#fff;border:0}
.sideCard{background:#fff;border:1px solid var(--line);border-radius:24px;padding:20px;height:max-content}.char{height:190px;background:#f0f2ff;border-radius:20px;display:grid;place-items:center;margin-bottom:14px}.char svg{height:170px}.sideName{font-weight:900;font-size:19px}.sideSmall{font-size:12px;color:var(--muted)}.statRow{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:16px}.stat{background:#f6f7fa;border-radius:13px;padding:10px}.stat b{font-size:20px;display:block}.stat small{color:var(--muted)}
/* finish */
.finish{min-height:calc(100vh - 130px);display:grid;place-items:center;text-align:center}.finishCard{width:min(780px,100%);background:#fff;border:1px solid var(--line);border-radius:32px;padding:40px;box-shadow:0 25px 70px #27345116}.seal{width:90px;height:90px;border-radius:50%;background:#eef0ff;color:#5264d4;display:grid;place-items:center;margin:auto;font-family:Changa;font-size:30px;font-weight:900}.finish h1{font-family:Changa;font-size:43px;margin:15px 0 5px}.resultGrid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin:25px 0}.resultStat{background:#f6f7fa;border-radius:17px;padding:14px}.resultStat b{font-size:25px;display:block}.certificate{border:2px solid #d9c687;border-radius:20px;padding:22px;background:#fffdf4;margin:20px auto;max-width:570px}.certificate h2{font-family:Changa;font-size:30px;margin:5px}
@media(max-width:850px){.welcome{grid-template-columns:1fr;padding:25px}.gameLayout{grid-template-columns:1fr}.sideCard{display:flex;gap:15px;align-items:center}.char{width:100px;height:100px;margin:0}.char svg{height:90px}.statRow{margin-top:0}.meter{display:none}.levels{grid-template-columns:repeat(3,1fr)}}
@media(max-width:560px){main{padding:14px}.top{padding:0 14px}.welcome{padding:20px}.levels{grid-template-columns:repeat(2,1fr)}.map{padding:18px}.choiceGrid{grid-template-columns:1fr}.gameHead{flex-wrap:wrap}.timer{margin-right:auto}.board{padding:20px}.finishCard{padding:24px}.resultGrid{grid-template-columns:1fr 1fr}.intro h1{font-size:45px}}
</style>
</head>
<body>
<div class="shell">
<header class="top">
  <div class="mark"><div class="markIcon">ن</div>رحلة النحو</div>
  <div class="userMini"><div class="miniAvatar" id="topAvatar">—</div><span id="topName">ابدئي رحلتك</span></div>
</header>

<main>
<section id="welcome" class="page active">
<div class="welcome">
<div class="intro">
<span class="pill">لعبة قواعد اللغة العربية · الصف الثالث</span>
<h1>جاهزة<br>لرحلة النحو؟</h1>
<p>هنا القاعدة مش مجرد معلومة تحفظيها… كل مستوى بيحوّلها إلى تحديات وتطبيق واكتشاف.</p>
<div style="margin-top:22px;color:#667188;font-size:13px;font-weight:700">المستوى الأول · أنواع الكلمة</div>
</div>
<div class="form">
<label>اكتبي اسمك</label><input id="studentName" placeholder="مثال: سلمى">
<label style="margin-top:20px">اختاري شخصيتك</label>
<div class="genderRow">
<button class="gender" data-g="boy">
<svg viewBox="0 0 120 130"><circle cx="60" cy="42" r="25" fill="#f3c7a6"/><path d="M35 41Q38 12 63 17Q86 14 87 43L77 31Q60 43 43 31Z" fill="#28324b"/><path d="M33 82Q60 62 87 82L96 126H24Z" fill="#4f65c9"/><circle cx="51" cy="43" r="3"/><circle cx="69" cy="43" r="3"/></svg><span>ولد</span>
</button>
<button class="gender" data-g="girl">
<svg viewBox="0 0 120 130"><circle cx="60" cy="43" r="25" fill="#f3c7a6"/><path d="M34 52Q25 14 60 12Q95 15 87 56L78 35Q60 25 42 37Z" fill="#5a3b42"/><path d="M32 84Q60 65 88 84L98 126H22Z" fill="#7866d9"/><circle cx="51" cy="44" r="3"/><circle cx="69" cy="44" r="3"/></svg><span>بنت</span>
</button>
</div>
<button id="begin" class="primary" style="width:100%" disabled>دخول الرحلة</button>
</div>
</div>
</section>

<section id="mapPage" class="page">
<div class="mapHead"><div><h2>خريطة الرحلة</h2><p>12 مستوى… وكل مستوى يفتح الطريق للي بعده.</p></div><span class="pill">الصف الثالث · الترم الأول</span></div>
<div class="map">
<div class="path"></div>
<div class="levels" id="levels"></div>
</div>
<div class="startLevel"><button class="primary" id="openLevel">دخول المستوى الأول</button></div>
</section>

<section id="gamePage" class="page">
<div class="gameHead">
<button class="back" id="backMap">الخريطة</button>
<div class="gameTitle"><b>المستوى الأول</b><h2>أنواع الكلمة</h2></div>
<div class="meter"><div class="meterTop"><span id="qText">1 / 7</span><span id="scoreText">0 نقطة</span></div><div class="meterBar"><div class="meterFill" id="fill"></div></div></div>
<div class="timer" id="timer">—</div>
</div>
<div class="gameLayout">
<div class="board">
<div><span class="boardTag" id="challengeTag">تحدي 01</span><h2 id="challengeTitle"></h2><p class="boardDesc" id="challengeDesc"></p></div>
<div class="stage" id="stage"></div>
<div class="feedback" id="feedback">ابدئي التحدي.</div>
<div class="nav"><button id="prev">السابق</button><button id="hint">تلميح</button><button class="next" id="next">التالي</button></div>
</div>
<aside class="sideCard">
<div class="char" id="gameChar"></div>
<div class="sideName" id="gameName"></div><div class="sideSmall">مغامرة النحو · المستوى 01</div>
<div class="statRow"><div class="stat"><b id="pts">0</b><small>النقاط</small></div><div class="stat"><b id="tries">0</b><small>المحاولات</small></div></div>
</aside>
</div>
</section>

<section id="finishPage" class="page">
<div class="finish"><div class="finishCard">
<div class="seal">✓</div>
<h1>المستوى اكتمل!</h1><p style="color:var(--muted)">أحسنتِ يا <b id="finishName"></b> — أول خطوة في الرحلة تمت بنجاح.</p>
<div class="resultGrid"><div class="resultStat"><b id="finalPoints">0</b><small>النقاط</small></div><div class="resultStat"><b id="finalTries">0</b><small>المحاولات</small></div><div class="resultStat"><b>01</b><small>المستوى المكتمل</small></div></div>
<div class="certificate"><div style="font-weight:800;color:#9b7b28">شهادة إتمام المستوى</div><h2 id="certName"></h2><p>أتمّ المستوى الأول في <b>أنواع الكلمة</b> ضمن رحلة النحو للصف الثالث الابتدائي.</p><b>إعداد الأستاذة شهد سعد عودة</b></div>
<button class="primary" id="mapAgain">العودة إلى خريطة الرحلة</button>
</div></div>
</section>
</main>
</div>

<script>
const levels=['أنواع الكلمة','أنواع الفعل','أنواع الحروف','أسماء الإشارة','ضمائر المتكلم','ضمائر المخاطب','ضمائر الغائب','أسلوب النهي','أسلوب النفي','أسلوب النداء','أسلوب التعجب','علامات الترقيم'];
const tasks=[
{type:'class',title:'فرّقي بين الأنواع',desc:'اضغطي على كل كلمة واختاري نوعها: اسم أم فعل أم حرف؟',hint:'الاسم يدل على شخص أو شيء، والفعل يدل على حدث، والحرف يربط بين الكلمات.',words:[['مدرسة','اسم'],['كتبَ','فعل'],['في','حرف'],['قلم','اسم'],['يلعبُ','فعل'],['من','حرف']]},
{type:'pick',title:'اختاري الكلمة',desc:'أمامك أربع كلمات. اختاري الكلمة التي تُعدّ فعلًا.',hint:'ابحثي عن كلمة تدل على عمل أو حدث.',opts:['الكتاب','يقرأُ','في','النافذة'],correct:1},
{type:'pick',title:'الاسم وسط الجملة',desc:'في: «ذهبَ سامرٌ إلى المدرسةِ» — اختاري اسم الشخص.',hint:'إنه اسم علم لشخص.',opts:['ذهبَ','سامرٌ','إلى','المدرسةِ'],correct:1},
{type:'pick',title:'صح أم خطأ؟',desc:'«في» اسم لأنها تدل على مكان.',hint:'«في» من حروف الجر.',opts:['صح','خطأ'],correct:1},
{type:'pick',title:'أكملي التصنيف',desc:'ما نوع كلمة «يلعبُ»؟',hint:'الكلمة تدل على عمل يحدث.',opts:['اسم','فعل','حرف'],correct:1},
{type:'write',title:'تحدي الكتابة',desc:'اكتبي جملة مفيدة تحتوي على اسم + فعل + حرف.',hint:'ابحثي عن جملة فيها عمل، واسم، وحرف مثل «في» أو «إلى».',correct:1},
{type:'pick',title:'التحدي الأخير',desc:'ما نوع الكلمات بالترتيب؟ «الولدُ — يكتبُ — في»',hint:'شخص/شيء، ثم عمل، ثم كلمة تربط.',opts:['اسم — فعل — حرف','فعل — اسم — حرف','اسم — حرف — فعل'],correct:0}
];
let name='',gender='',task=0,score=0,tries=0,solved=Array(7).fill(false),answers=Array(7).fill(null),time=0,timerId;

function show(id){document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));document.getElementById(id).classList.add('active');window.scrollTo(0,0)}
function character(g='boy',small=false){return `<svg viewBox="0 0 120 150" style="height:${small?'125px':'165px'}"><circle cx="60" cy="48" r="29" fill="#f3c7a6"/><path d="${g==='girl'?'M30 58Q22 14 60 12Q98 15 90 62L78 35Q60 24 42 38Z':'M31 47Q34 12 64 16Q91 15 89 49L78 35Q60 45 42 32Z'}" fill="${g==='girl'?'#5a3b42':'#28324b'}"/><path d="M28 91Q60 68 92 91L103 146H17Z" fill="${g==='girl'?'#7866d9':'#4f65c9'}"/><circle cx="50" cy="49" r="3"/><circle cx="70" cy="49" r="3"/><path d="M50 64Q60 70 70 64" fill="none" stroke="#9e5d5d" stroke-width="2"/></svg>`}
document.querySelectorAll('.gender').forEach(b=>b.onclick=()=>{gender=b.dataset.g;document.querySelectorAll('.gender').forEach(x=>x.classList.remove('selected'));b.classList.add('selected');validate()});
document.getElementById('studentName').oninput=validate;
function validate(){document.getElementById('begin').disabled=!(document.getElementById('studentName').value.trim()&&gender)}
document.getElementById('begin').onclick=()=>{name=document.getElementById('studentName').value.trim();document.getElementById('topName').textContent=name;document.getElementById('topAvatar').innerHTML=character(gender,true);buildMap();show('mapPage')};
function buildMap(){document.getElementById('levels').innerHTML=levels.map((x,i)=>`<div class="level ${i===0?'current':''} ${i>0?'locked':''}"><div class="node">${i===0?'01':i+1}</div><div class="levelName">${x}</div><div class="levelSub">${i===0?'متاح الآن':'مغلق'}</div></div>`).join('')}
document.getElementById('openLevel').onclick=()=>{document.getElementById('gameName').textContent=name;document.getElementById('gameChar').innerHTML=character(gender);renderTask();show('gamePage')};
document.getElementById('backMap').onclick=()=>show('mapPage');
document.getElementById('mapAgain').onclick=()=>show('mapPage');
function renderTask(){
clearInterval(timerId);let t=tasks[task];time=t.type==='write'?70:35;
document.getElementById('timer').textContent=time+'ث';document.getElementById('timer').classList.remove('low');
document.getElementById('qText').textContent=(task+1)+' / '+tasks.length;document.getElementById('scoreText').textContent=score+' نقطة';document.getElementById('fill').style.width=((task)/tasks.length*100)+'%';
document.getElementById('challengeTag').textContent='تحدي '+String(task+1).padStart(2,'0');document.getElementById('challengeTitle').textContent=t.title;document.getElementById('challengeDesc').textContent=t.desc;
document.getElementById('feedback').className='feedback';document.getElementById('feedback').textContent=solved[task]?'تم حل التحدي. يمكنك مراجعته.':'اختاري إجابتك.';
let s='';
if(t.type==='class')s=`<div class="words">${t.words.map((w,i)=>`<button class="word" onclick="cycle(${i})">${w[0]}<small style="display:block;font-size:11px;color:#8b93a5;margin-top:5px">${answers[task]?.[i]||'اضغطي للتصنيف'}</small></button>`).join('')}</div>`;
else if(t.type==='pick')s=`<div class="choiceGrid">${t.opts.map((o,i)=>`<button class="choice" onclick="choose(${i})">${o}</button>`).join('')}</div>`;
else s=`<div class="write"><textarea id="writing" placeholder="اكتبي جملتك هنا…"></textarea><div class="textareaActions"><button class="primary" onclick="checkWriting()">تحقق من الإجابة</button></div></div>`;
document.getElementById('stage').innerHTML=s;document.getElementById('pts').textContent=score;document.getElementById('tries').textContent=tries;
timerId=setInterval(()=>{time--;document.getElementById('timer').textContent=time+'ث';if(time<=8)document.getElementById('timer').classList.add('low');if(time<=0){clearInterval(timerId);feedback('انتهى الوقت. خدي تلميحًا وحاولي مرة أخرى.','bad')}},1000);
}
function cycle(i){if(solved[task])return;let a=answers[task]||Array(6).fill(null);a[i]=a[i]===null?'اسم':a[i]==='اسم'?'فعل':a[i]==='فعل'?'حرف':null;answers[task]=a;if(a.every(Boolean)){tries++;let ok=a.every((v,j)=>v===tasks[0].words[j][1]);if(ok){score+=20;solved[task]=true;feedback('ممتاز! كل التصنيفات صحيحة. +20 نقطة','good')}else feedback('لسه في كلمة محتاجة مراجعة. جرّبي تاني.','bad')}renderTask()}
function choose(i){if(solved[task])return;tries++;let t=tasks[task];if(i===t.correct){score+=15;solved[task]=true;feedback('إجابة صحيحة. أحسنتِ! +15 نقطة','good')}else feedback('ليست الإجابة الصحيحة. جرّبي مرة أخرى.','bad');renderTask()}
function checkWriting(){if(solved[task])return;let v=document.getElementById('writing').value.trim();tries++;let words=v.split(/\s+/).filter(Boolean);let verb=/(كتب|يكتب|قرأ|يقرأ|ذهب|يذهب|لعب|يلعب|جلس|يجلس|أكل|يأكل|شرب|يشرب|رسم|يرسم|نام|ينام|فتح|يفتح|عاد|يعود|نجح|ينجح)/.test(v);let prep=/(في|من|إلى|عن|على|بـ|كـ|لـ)/.test(v);if(words.length>=3&&verb&&prep){score+=20;solved[task]=true;feedback('جملة رائعة! فيها اسم وفعل وحرف. +20 نقطة','good');renderTask()}else feedback('راجعي الجملة: نحتاج اسمًا وفعلًا وحرفًا.','bad')}
function feedback(t,c){let e=document.getElementById('feedback');e.textContent=t;e.className='feedback '+c}
document.getElementById('hint').onclick=()=>feedback('تلميح: '+tasks[task].hint,'hint');
document.getElementById('prev').onclick=()=>{if(task>0){task--;renderTask()}};
document.getElementById('next').onclick=()=>{if(!solved[task]){feedback('حلّي التحدي قبل الانتقال.','bad');return}if(task<tasks.length-1){task++;renderTask()}else finish()};
function finish(){clearInterval(timerId);document.getElementById('finalPoints').textContent=score;document.getElementById('finalTries').textContent=tries;document.getElementById('finishName').textContent=name;document.getElementById('certName').textContent=name;show('finishPage')}
</script>
</body>
</html>'''
path=Path("/mnt/data/nahw-grade3-level1-v2.html")
path.write_text(html,encoding="utf-8")
print(path)
