<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Interactiv: Istoria Limbii Române</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@700&family=EB+Garamond&display=swap" rel="stylesheet">
<style>
body { font-family: 'Cinzel', sans-serif; margin: 20px; background-color: #C4A484; }
h1 { color: #3B2F2F; }
.question { margin-bottom: 25px; padding: 15px; background: #fff; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); }
.option { display: block; margin: 8px 0; padding: 8px; border: 1px solid #ccc; border-radius: 5px; cursor: pointer; }
.option.correct { background-color: #c8e6c9; border-color: #008000; }
.option.wrong { background-color: #ffcdd2; border-color: #FF0000; }
#result { margin-top: 20px; font-weight: bold; font-size: 1.2em; }
.matching { display: flex; justify-content: space-between; }
.match-column { display: flex; flex-direction: column; gap: 10px; }
.draggable { padding: 8px; border: 1px solid #666; border-radius: 5px; background: #eee; cursor: grab; }
.droppable { padding: 10px; min-height: 40px; border: 2px dashed #aaa; border-radius: 5px; background: #fafafa; }
</style>
</head>
<body>


<h1>Quiz Interactiv: Istoria Limbii Române</h1>

<div class="question" data-answer="true">
<p>1. Limba română provine din limba latină.</p>
<span class="option"data-value="true">Adevărat</span>
<span class="option" data-value="false">Fals</span>
</div>

<div class="question" data-answer="false">
<p>2. Alfabetul limbii române a fost întotdeauna cel latin.</p>
<span class="option" data-value="true">Adevărat</span>
<span class="option" data value="false">Fals</span>
</div>

<div class="question" data-answer="false">
<p>3. Limba română a fost influențată doar de limba latină.</p>
<span class="option" data-value="true">Adevărat</span>
<span class="option" data-value="false">Fals</span>
</div>

<div class="question" data-answer="true">
<p>4.Substratul limbii române este substratul geto-dac.</p>
<span class="option" data-value="true">Adevărat</span>
<span class="option" data-value="false">Fals</span>
</div>

<div class="question" data-answer="c">
<p>5.În ce an a fost cucerita Dacia de catre romani, fapt care a rezultat la romanizarea Daciei</p>
<span class="option" data-value="a">101 d.Hr</span>
<span class="option" data-value="b">102 d.Hr</span>
<span class="option" data-value="c">106 d.Hr</span>
<span class="option" data-value="d">106 î.HR</span>

</div>

<div class="question" data-answer="c">
<p>6. În ce secol au început să apară primele texte scrise în limba română?</p>
<span class="option" data-value="a">Secolul IX</span>
<span class="option" data-value="b">Secolul XI</span>
<span class="option" data-value="c">Secolul XVI</span>
<span class="option" data-value="d">Secolul XIX</span>
</div>

<div class="question" data-answer="c">
<p>7.În ce perioada istorică limba romănă a avut alfabet chirilic? </p>
<span class="option" data-value="a">Epoca Antică</span>
<span class="option" data-value="b">Epoca Contemporană</span>
<span class="option" data-value="c">Epoca Medievală</span>
<span class="option" data-value="d">Epoca Modernă</span>
</div>




<p>8. Potrivește termenii cu definițiile lor (drag & drop):</p>
<div class="matching">
<div class="match-column">
<div class="draggable" draggable="true" id="latin">Limba latină</div>
<div class="draggable" draggable="true" id="slav">Limba slavă</div>
<div class="draggable" draggable="true" id="greek">Limba greacă</div>
<div class="draggable" draggable="true" id="scl">Apariția Școlii Ardelene</div>
<div class="draggable" draggable="true" id="neo">Neologisme(franceză și engleză)</div>
<div class="draggable" draggable="true" id="clasici">Marii Clasici</div>
</div>
<div class="match-column">
<div class="droppable" data-answer="latin">1. Este sursa principală a limbii române</div>
<div class="droppable" data-answer="slav">2. A influențat limba română veche prin biserică și literatură</div>
<div class="droppable" data-answer="greek">3. A adus cuvinte noi prin contact comercial și cultural</div>
<div class="droppable" data-answer="neo">4.Sec. XX</div>
<div class="droppable" data-answer="clasici">5.Sfârsitul sec. IX</div>
<div class="droppable" data-answer="scl">6.Sec XVIII</div>
</div>
</div>

<button id="checkBtn">Verifică răspunsurile</button>
<div id="result"></div>

<script>
let score = 0;

// Adevărat/Fals și Multiple Choice
document.querySelectorAll('.question').forEach(q => {
    q.querySelectorAll('.option').forEach(opt => {
        opt.addEventListener('click', () => {
            if(q.dataset.answer === opt.dataset.value || (opt.textContent.toLowerCase() === q.dataset.answer)) {
                opt.classList.add('correct');
                score++;
            } else {
                opt.classList.add('wrong');
            }
            q.querySelectorAll('.option').forEach(o => o.style.pointerEvents = 'none');
        });
    });
});

// Drag & Drop pentru Matching
const draggables = document.querySelectorAll('.draggable');
const droppables = document.querySelectorAll('.droppable');

draggables.forEach(d => {
    d.addEventListener('dragstart', e => { e.dataTransfer.setData('text', d.id); });
});

droppables.forEach(drop => {
    drop.addEventListener('dragover', e => e.preventDefault());
    drop.addEventListener('drop', e => {
        e.preventDefault();
        const id = e.dataTransfer.getData('text');
        if(id === drop.dataset.answer) {
            drop.textContent = document.getElementById(id).textContent;
            drop.style.backgroundColor = '#c8e6c9';
            score++;
        } else {
            drop.style.backgroundColor = '#ffcdd2';
        }
    });
});

document.getElementById('checkBtn').addEventListener('click', () => {
    document.getElementById('result').textContent = "Scorul tău final: " + score + " / ";
});
</script>

</body>
</html>
