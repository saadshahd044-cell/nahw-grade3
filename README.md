from pathlib import Path

html = r'''<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Level 01 — أنواع الكلمة</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@500;600;700;800;900&family=Tajawal:wght@500;700;800&display=swap');
:root{
  --bg:#f4f7fb; --ink:#172033; --muted:#738096; --card:#fff; --line:#e6ebf2;
  --primary:#5867e8; --primary2:#7b62d8; --cyan:#38b8c9; --green:#2fb27f;
  --orange:#f2a64b; --red:#e96a78; --shadow:0 18px 50px rgba(37,52,82,.12);
}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(circle at 15% 0,#e9edff 0 20%,transparent 40%),linear-gradient(135deg,#f7f9fc,#eef3f9);color:var(--ink);font-family:Cairo,Tajawal,sans-serif;min-height:100vh}
button,input{font:inherit}
button{cursor:pointer}
.app{max-width:1180px;margin:auto;padding:18px}
.topbar{display:flex;align-items:center;gap:14px;margin-bottom:16px}
.brand{display:flex;align-items:center;gap:10px;font-weight:900}
.logo{width:44px;height:44px;border-radius:15px;background:linear-gradient(145deg,var(--primary),var(--primary2));color:#fff;display:grid;place-items:center;font-size:22px;box-shadow:0 10px 24px #6570dc44}
.progressWrap{flex:1;background:#fff;border:1px solid var(--line);border-radius:20px;padding:8px 12px;box-shadow:0 8px 25px #24344b0c}
.progressTop{display:flex;justify-content:space-between;font-size:12px;color:var(--muted);margin-bottom:6px}
.progress{height:9px;background:#edf0f6;border-radius:99px;overflow:hidden}
.bar{height:100%;width:0;background:linear-gradient(90deg,var(--primary),#8a67df);border-radius:99px;transition:.4s}
.timer{background:#fff;border:1px solid var(--line);border-radius:16px;padding:10px 14px;font-weight:900;box-shadow:0 8px 25px #24344b0c;min-width:88px;text-align:center}
.timer.warn{color:var(--red);animation:pulse .8s infinite}
@keyframes pulse{50%{transform:scale(1.04)}}

.screen{display:none}.screen.active{display:block;animation:enter .45s ease}
@keyframes enter{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.hero{background:linear-gradient(135deg,#202a57,#4855b9 58%,#7963cf);color:#fff;border-radius:30px;padding:34px;box-shadow:var(--shadow);position:relative;overflow:hidden}
.hero:after{content:"";position:absolute;width:260px;height:260px;border:50px solid #ffffff12;border-radius:50%;left:-90px;top:-100px}
.eyebrow{font-size:13px;opacity:.75;font-weight:800}.hero h1{font-size:clamp(30px,5vw,55px);margin:6px 0}.hero p{margin:0;color:#e9ecff}
.formCard{margin-top:18px;background:#fff;border:1px solid var(--line);border-radius:26px;padding:25px;box-shadow:var(--shadow)}
.row{display:flex;gap:12px;flex-wrap:wrap}.field{flex:1;min-width:220px}
label{display:block;font-weight:800;margin-bottom:8px}input[type=text]{width:100%;padding:15px 16px;border:2px solid var(--line);border-radius:16px;outline:none}input:focus{border-color:var(--primary)}
.gender{display:flex;gap:10px}.gender button{flex:1;border:2px solid var(--line);background:#fff;border-radius:16px;padding:13px;font-weight:800}.gender button.sel{border-color:var(--primary);background:#f1f2ff;color:#4e58ca}
.primary{border:0;background:linear-gradient(135deg,var(--primary),var(--primary2));color:#fff;padding:14px 22px;border-radius:16px;font-weight:900;box-shadow:0 12px 25px #5867e844}.primary:disabled{opacity:.5;cursor:not-allowed}

.gameGrid{display:grid;grid-template-columns:1fr 330px;gap:18px}
@media(max-width:850px){.gameGrid{grid-template-columns:1fr}.side{order:-1}}
.challenge,.side{background:#fff;border:1px solid var(--line);border-radius:28px;box-shadow:var(--shadow)}
.challenge{padding:26px;min-height:590px;display:flex;flex-direction:column}
.side{padding:20px;height:max-content}
.badge{display:inline-flex;align-items:center;gap:7px;background:#f0f2ff;color:#505dcc;border-radius:99px;padding:7px 11px;font-size:12px;font-weight:900;width:max-content}
.challenge h2{font-size:clamp(24px,4vw,36px);margin:14px 0 7px}.desc{color:var(--muted);margin:0 0 20px}
.stage{flex:1;display:flex;align-items:center;justify-content:center}
.cards{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;width:100%;max-width:680px}
.word{min-height:110px;border:2px solid var(--line);background:#fff;border-radius:22px;font-size:23px;font-weight:900;box-shadow:0 8px 18px #24344b0b;transition:.2s}
.word:hover{transform:translateY(-4px);border-color:#8e98ed}.word.selected{border-color:var(--primary);background:#f0f2ff}.word.correct{border-color:var(--green);background:#eafaf3;animation:pop .35s}.word.wrong{border-color:var(--red);background:#fff0f2;animation:shake .35s}
@keyframes pop{50%{transform:scale(1.06)}} @keyframes shake{25%{transform:translateX(6px)}75%{transform:translateX(-6px)}}
.feedback{min-height:46px;border-radius:16px;padding:11px 14px;margin-top:15px;font-weight:800;background:#f7f8fb;color:var(--muted)}.feedback.good{background:#eafaf3;color:#187653}.feedback.bad{background:#fff0f2;color:#b83e4e}.feedback.hint{background:#fff8e9;color:#9b681d}
.actions{display:flex;justify-content:space-between;gap:10px;margin-top:15px}.secondary{border:1px solid var(--line);background:#fff;border-radius:15px;padding:12px 18px;font-weight:800}.secondary:disabled{opacity:.35}
.side h3{margin-top:0}.avatar{width:72px;height:72px;border-radius:23px;background:#f1f2ff;display:grid;place-items:center;font-size:38px;margin-bottom:10px}
.stats{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-top:15px}.stat{background:#f7f8fb;border-radius:16px;padding:12px}.stat b{display:block;font-size:20px}.stat small{color:var(--muted)}
.miniMap{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-top:14px}.dot{height:43px;border-radius:13px;display:grid;place-items:center;font-weight:900;background:#edf0f5;color:#9aa4b5}.dot.current{background:#5968e8;color:#fff;box-shadow:0 7px 16px #5968e844}.dot.done{background:#e8f8f1;color:#258260}
.choiceGrid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;width:100%;max-width:700px}.choice{padding:18px;border:2px solid var(--line);border-radius:19px;background:#fff;font-weight:900;font-size:19px}.choice:hover{border-color:#8992eb}.choice.correct{background:#eafaf3;border-color:var(--green)}.choice.wrong{background:#fff0f2;border-color:var(--red)}
.sentence{background:#f7f8fb;border:1px dashed #ccd3df;border-radius:22px;padding:25px;text-align:center;font-size:28px;font-weight:900;max-width:700px;width:100%}
.blank{color:var(--primary);border-bottom:3px solid var(--primary);padding:0 18px}
textarea{width:100%;min-height:125px;border:2px solid var(--line);border-radius:18px;padding:15px;resize:none;outline:none}.textareaWrap{width:100%;max-width:700px}
.result{text-align:center;padding:35px}.score{font-size:64px;font-weight:900;color:var(--primary)}.stars{font-size:38px;letter-spacing:5px}.certificate{margin:20px auto;padding:26px;max-width:620px;border:2px solid #d9c27c;border-radius:24px;background:linear-gradient(135deg,#fffdf5,#fff);box-shadow:var(--shadow)}
.hidden{display:none!important}
@media(max-width:620px){.app{padding:10px}.hero{padding:24px;border-radius:24px}.cards,.choiceGrid{grid-template-columns:1fr}.challenge{padding:18px;min-height:560px}.topbar{flex-wrap:wrap}.progressWrap{order:3;flex-basis:100%}.timer{margin-right:auto}.word{min-height:82px}.sentence{font-size:22px}}
</style>
</head>
<body>
<div class="app">
  <div class="topbar">
    <div class="brand"><div class="logo">ن</div><div>رحلة النحو</div></div>
    <div class="progressWrap"><div class="progressTop"><span id="qLabel">جاهز</span><span id="scoreLabel">0 نقطة</span></div><div class="progress"><div class="bar" id="bar"></div></div></div>
    <div class="timer" id="timer">—</div>
  </div>

  <section id="intro" class="screen active">
    <div class="hero">
      <div class="eyebrow">LEVEL 01 • البداية</div>
      <h1>أنواع الكلمة</h1>
      <p>اسم؟ فعل؟ حرف؟ خلّي عينك سريعة… وابدأ التحدي.</p>
    </div>
    <div class="formCard">
      <div class="row">
        <div class="field"><label>اسمك إيه؟</label><input id="name" type="text" placeholder="اكتب اسمك هنا"></div>
        <div class="field"><label>اختار شخصيتك</label><div class="gender"><button data-g="boy">👦 ولد</button><button data-g="girl">👧 بنت</button></div></div>
      </div>
      <div style="margin-top:18px;display:flex;justify-content:flex-start"><button id="start" class="primary" disabled>ابدأ Level 01 🚀</button></div>
    </div>
  </section>

  <section id="game" class="screen">
    <div class="gameGrid">
      <main class="challenge">
        <div><span class="badge" id="typeBadge">تحدي 1</span><h2 id="title"></h2><p class="desc" id="desc"></p></div>
        <div class="stage" id="stage"></div>
        <div id="feedback" class="feedback">اختار إجابتك.</div>
        <div class="actions"><button class="secondary" id="prev">← السابق</button><button class="secondary" id="hint">💡 تلميح</button><button class="primary" id="next">التالي →</button></div>
      </main>
      <aside class="side">
        <div class="avatar" id="avatar">👦</div><b id="playerName">الطالب</b><div style="color:var(--muted);font-size:13px">Level 01 · أنواع الكلمة</div>
        <div class="stats"><div class="stat"><b id="points">0</b><small>النقاط</small></div><div class="stat"><b id="attempts">0</b><small>المحاولات</small></div></div>
        <h3 style="margin-bottom:7px">تقدمك</h3><div class="miniMap" id="miniMap"></div>
      </aside>
    </div>
  </section>

  <section id="result" class="screen">
    <div class="result">
      <div class="hero"><div class="eyebrow">LEVEL COMPLETE</div><h1>أحسنت يا <span id="finalName"></span>! 🎉</h1><p>أنت خلّصت أول تحديات رحلة النحو.</p></div>
      <div class="score" id="finalScore">0</div><div class="stars" id="finalStars">★★★</div>
      <div class="certificate"><div style="font-weight:900;font-size:22px">شهادة إتمام المستوى</div><p>تشهد رحلة النحو بأن</p><h2 id="certName"></h2><p>أتمّ <b>المستوى الأول: أنواع الكلمة</b> بنجاح.</p><b>إعداد الأستاذة شهد سعد عودة</b></div>
      <button class="primary" onclick="location.reload()">إعادة اللعب 🔄</button>
    </div>
  </section>
</div>

<script>
const tasks = [
 {kind:'classify',title:'رتّب الكلمات',desc:'صنّف كل كلمة في مكانها الصحيح.',hint:'الاسم يدل على شخص أو شيء، والفعل يدل على حدث، والحرف يربط بين الكلمات.',data:[
  ['مدرسة','اسم'],['كتبَ','فعل'],['في','حرف'],['قلم','اسم'],['يلعبُ','فعل'],['من','حرف']
 ]},
 {kind:'pick',title:'اصطد النوع المطلوب',desc:'اضغط على الكلمة التي تُعدّ فعلًا.',hint:'ابحث عن كلمة تدل على حدث أو عمل.',data:['الكتاب','يقرأُ','على','النافذة']},
 {kind:'sentence',title:'اقرأ الجملة بذكاء',desc:'في الجملة: «ذهبَ سامرٌ إلى المدرسةِ». اختر الاسم.',hint:'الاسم هنا اسم شخص.',data:['ذهبَ','سامرٌ','إلى','المدرسةِ']},
 {kind:'tf',title:'صح أم خطأ؟',desc:'«في» اسم لأنها تدل على مكان.',hint:'في من حروف الجر.',data:['صح','خطأ'],correct:1},
 {kind:'complete',title:'أكمل التصنيف',desc:'اختر النوع المناسب للكلمة: «يلعبُ».',hint:'الكلمة تدل على عمل يحدث.',data:['اسم','فعل','حرف'],correct:1},
 {kind:'write',title:'تحدي الكتابة ✏️',desc:'اكتب جملة مفيدة تحتوي على: اسم + فعل + حرف.',hint:'مثال للتفكير فقط: ابحث عن جملة فيها من فعل شيئًا، ويوجد فيها حرف مثل «في» أو «إلى».',data:[]},
 {kind:'final',title:'التحدي النهائي 🏆',desc:'اختبر سرعتك: ما نوع الكلمات الثلاث بالترتيب؟ «الولدُ — يكتبُ — في».',hint:'فكّر: شخص/شيء، ثم عمل، ثم كلمة تربط.',data:['اسم — فعل — حرف','فعل — اسم — حرف','اسم — حرف — فعل'],correct:0}
];
let idx=0, points=0, attempts=0, selectedGender='', answers=Array(tasks.length).fill(null), solved=Array(tasks.length).fill(false), time=45, interval;
const $=id=>document.getElementById(id);
document.querySelectorAll('[data-g]').forEach(b=>b.onclick=()=>{selectedGender=b.dataset.g;document.querySelectorAll('[data-g]').forEach(x=>x.classList.remove('sel'));b.classList.add('sel');$('start').disabled=!$('name').value.trim()});
$('name').oninput=()=>{$('start').disabled=!$('name').value.trim()||!selectedGender};
$('start').onclick=()=>{ $('intro').classList.remove('active');$('game').classList.add('active');$('playerName').textContent=$('name').value.trim();$('avatar').textContent=selectedGender==='girl'?'👧':'👦';renderMap();render(); };
$('prev').onclick=()=>{if(idx>0){idx--;render()}};
$('next').onclick=()=>{if(!solved[idx]){showFeedback('حلّي التحدي الأول ثم انتقلي.', 'bad');return} if(idx<tasks.length-1){idx++;render()}else finish()};
$('hint').onclick=()=>showFeedback('💡 '+tasks[idx].hint,'hint');
function renderMap(){ $('miniMap').innerHTML=tasks.map((_,i)=>`<div class="dot ${i===idx?'current':''} ${solved[i]?'done':''}">${solved[i]?'✓':i+1}</div>`).join(''); }
function render(){
 clearInterval(interval);time=tasks[idx].kind==='write'?75:45;
 $('timer').textContent=time+'ث';$('timer').classList.remove('warn');
 $('qLabel').textContent=`تحدي ${idx+1} من ${tasks.length}`;$('scoreLabel').textContent=points+' نقطة';
 $('points').textContent=points;$('attempts').textContent=attempts;$('bar').style.width=((idx)/tasks.length*100)+'%';
 $('typeBadge').textContent='تحدي '+(idx+1);$('title').textContent=tasks[idx].title;$('desc').textContent=tasks[idx].desc;
 $('feedback').className='feedback';$('feedback').textContent=solved[idx]?'✓ تم حل التحدي. يمكنك مراجعته أو الانتقال.':'اختار إجابتك.';
 const t=tasks[idx]; let s='';
 if(t.kind==='classify') s=`<div style="width:100%;max-width:700px"><div class="cards">${t.data.map((x,i)=>`<button class="word ${answers[idx]?.[i]?'selected':''}" onclick="cycleClass(${i})">${x[0]}<small style="display:block;color:#8a94a5;font-size:12px;margin-top:5px">${answers[idx]?.[i]||'اضغط للتصنيف'}</small></button>`).join('')}</div><div style="margin-top:12px;text-align:center;color:#7a8497;font-size:13px">كل ضغطة تغيّر النوع: اسم ← فعل ← حرف</div></div>`;
 if(t.kind==='pick'||t.kind==='sentence') s=`<div class="${t.kind==='sentence'?'choiceGrid':'cards'}">${t.data.map((x,i)=>`<button class="choice ${answers[idx]===i?'selected':''}" onclick="choose(${i})">${x}</button>`).join('')}</div>`;
 if(t.kind==='tf'||t.kind==='complete'||t.kind==='final') s=`<div class="choiceGrid">${t.data.map((x,i)=>`<button class="choice" onclick="choose(${i})">${x}</button>`).join('')}</div>`;
 if(t.kind==='write') s=`<div class="textareaWrap"><textarea id="answerText" placeholder="اكتب جملتك هنا…"></textarea><div style="margin-top:10px"><button class="primary" onclick="checkWrite()">تحقق من إجابتي ✓</button></div></div>`;
 $('stage').innerHTML=s;
 interval=setInterval(()=>{time--; $('timer').textContent=time+'ث'; if(time<=8)$('timer').classList.add('warn'); if(time<=0){clearInterval(interval);showFeedback('⏱️ انتهى الوقت. خدي تلميحًا وحاولي مرة أخرى.','bad')}},1000);
 renderMap();
}
function cycleClass(i){
 if(solved[idx])return;
 let a=answers[idx]||Array(tasks[idx].data.length).fill(null), cur=a[i];
 a[i]=cur===null?'اسم':cur==='اسم'?'فعل':cur==='فعل'?'حرف':null; answers[idx]=a;
 if(a.every(Boolean)){let ok=a.every((v,j)=>v===tasks[idx].data[j][1]);attempts++; if(ok){points+=15;solved[idx]=true;showFeedback('🎯 ممتاز! كل الكلمات في مكانها الصحيح.','good')}else{showFeedback('مش كلها صح… راجعي الكلمات وحاولي تاني.','bad')}} render();
}
function choose(i){
 if(solved[idx])return;
 attempts++; const t=tasks[idx], correct=t.correct!==undefined?t.correct:(t.kind==='pick'?1: t.kind==='sentence'?1:0);
 answers[idx]=i;
 if(i===correct){points+=15;solved[idx]=true;showFeedback('🎯 إجابة صحيحة! +15 نقطة','good')}else showFeedback('❌ مش دي… جرّبي مرة تانية 💡','bad');
 render();
}
function checkWrite(){
 const v=($('answerText').value||'').trim();
 attempts++;
 const words=v.split(/\s+/).filter(Boolean);
 const hasVerb=/(كتب|يكتب|قرأ|يقرأ|ذهب|يذهب|لعب|يلعب|جلس|يجلس|أكل|يأكل|شرب|يشرب|رسم|يرسم|نام|ينام|فتح|يفتح|عاد|يعود|نجح|ينجح)/.test(v);
 const hasPrep=/(في|من|إلى|عن|على|الباء|بـ|كـ|لـ|اللام)/.test(v);
 if(words.length>=3&&hasVerb&&hasPrep){points+=20;solved[idx]=true;answers[idx]=v;showFeedback('✨ جملة ممتازة! فيها فعل وحرف واسم/أسماء. +20 نقطة','good');render()}else showFeedback('✏️ الجملة محتاجة مراجعة بسيطة: تأكدي أن فيها فعلًا وحرفًا واسمًا.','bad');
}
function showFeedback(txt,cls){$('feedback').textContent=txt;$('feedback').className='feedback '+cls}
function finish(){
 clearInterval(interval);$('game').classList.remove('active');$('result').classList.add('active');$('bar').style.width='100%';
 const score=Math.min(points,100);$('finalScore').textContent=score+' نقطة';$('finalName').textContent=$('name').value.trim();$('certName').textContent=$('name').value.trim();
 $('finalStars').textContent=score>=85?'★★★':score>=60?'★★☆':'★☆☆';
}
</script>
</body>
</html>'''

path = Path("/mnt/data/level-01-anwa3-alkalima.html")
path.write_text(html, encoding="utf-8")
print(f"تم إنشاء الموقع: {path}")
