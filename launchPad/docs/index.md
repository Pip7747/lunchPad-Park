# Welcome to the Launch Pad Park

<style>
/* ===== Guitar chord sidebar (LEFT) ===== */
#piano-zone {
    position: fixed;
    left: 0;
    top: 0;
    width: 60px;
    height: 100%;
    z-index: 9999;
}

#piano-sidebar {
    position: fixed;
    left: -90px;
    top: 50%;
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;
    gap: 4px;
    transition: left 0.3s ease;
    z-index: 10000;
    padding: 10px 6px;
    background: rgba(30, 30, 30, 0.85);
    border-radius: 0 12px 12px 0;
    backdrop-filter: blur(6px);
}

#piano-zone:hover ~ #piano-sidebar,
#piano-sidebar:hover {
    left: 0;
}

.piano-key {
    width: 72px;
    height: 72px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 15px;
    color: #1a1a2e;
    transition: transform 0.1s, box-shadow 0.1s, filter 0.1s;
    box-shadow: 0 3px 8px rgba(0,0,0,0.25);
    user-select: none;
    text-shadow: 0 1px 1px rgba(255,255,255,0.3);
}

.piano-key:active,
.piano-key.playing {
    transform: scale(0.92);
    box-shadow: 0 1px 3px rgba(0,0,0,0.3);
    filter: brightness(1.15);
}

.piano-key:nth-child(1) { background: linear-gradient(135deg, #ff6b6b, #ee5a24); }
.piano-key:nth-child(2) { background: linear-gradient(135deg, #ffa502, #e67e22); }
.piano-key:nth-child(3) { background: linear-gradient(135deg, #ffd32a, #f0c419); }
.piano-key:nth-child(4) { background: linear-gradient(135deg, #7bed9f, #2ed573); }
.piano-key:nth-child(5) { background: linear-gradient(135deg, #70a1ff, #1e90ff); }
.piano-key:nth-child(6) { background: linear-gradient(135deg, #a29bfe, #6c5ce7); }

/* ===== Drum sidebar (RIGHT) ===== */
#drum-zone {
    position: fixed;
    right: 0;
    top: 0;
    width: 60px;
    height: 100%;
    z-index: 9999;
}

#drum-sidebar {
    position: fixed;
    right: -90px;
    top: 50%;
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;
    gap: 4px;
    transition: right 0.3s ease;
    z-index: 10000;
    padding: 10px 6px;
    background: rgba(30, 30, 30, 0.85);
    border-radius: 12px 0 0 12px;
    backdrop-filter: blur(6px);
}

#drum-zone:hover ~ #drum-sidebar,
#drum-sidebar:hover {
    right: 0;
}

.drum-key {
    width: 72px;
    height: 72px;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 12px;
    color: #fff;
    transition: transform 0.1s, box-shadow 0.1s, filter 0.1s;
    box-shadow: 0 3px 8px rgba(0,0,0,0.35);
    user-select: none;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.drum-key:active,
.drum-key.playing {
    transform: scale(0.88);
    box-shadow: 0 1px 3px rgba(0,0,0,0.4);
    filter: brightness(1.2);
}

.drum-key:nth-child(1) { background: radial-gradient(circle at 35% 35%, #e74c3c, #922b21); }
.drum-key:nth-child(2) { background: radial-gradient(circle at 35% 35%, #f39c12, #b7950b); }
.drum-key:nth-child(3) { background: radial-gradient(circle at 35% 35%, #2ecc71, #1a9850); }
.drum-key:nth-child(4) { background: radial-gradient(circle at 35% 35%, #3498db, #21618c); }
.drum-key:nth-child(5) { background: radial-gradient(circle at 35% 35%, #9b59b6, #6c3483); }
.drum-key:nth-child(6) { background: radial-gradient(circle at 35% 35%, #e67e22, #a04000); }

/* ===== Chord display overlay ===== */
#chord-display {
    position: fixed;
    left: 50%;
    top: 30%;
    transform: translate(-50%, -50%);
    font-size: 64px;
    font-weight: 800;
    opacity: 0;
    transition: opacity 0.2s, transform 0.3s;
    pointer-events: none;
    z-index: 10001;
    text-shadow: 0 2px 20px rgba(0,0,0,0.2);
}

#chord-display.show {
    opacity: 1;
    transform: translate(-50%, -55%);
}

/* ===== Drum display overlay ===== */
#drum-display {
    position: fixed;
    left: 50%;
    top: 45%;
    transform: translate(-50%, -50%);
    font-size: 42px;
    font-weight: 700;
    opacity: 0;
    transition: opacity 0.15s, transform 0.2s;
    pointer-events: none;
    z-index: 10001;
    text-shadow: 0 2px 15px rgba(0,0,0,0.3);
    color: #e74c3c;
}

#drum-display.show {
    opacity: 1;
    transform: translate(-50%, -55%);
}

/* ===== Song cards ===== */
.song-card {
    background: linear-gradient(135deg, #1a1a2e, #16213e);
    border-radius: 12px;
    padding: 18px 22px;
    margin: 12px 0;
    color: #eee;
    border-left: 4px solid;
    transition: transform 0.2s, box-shadow 0.2s;
}
.song-card:hover {
    transform: translateX(4px);
    box-shadow: 0 4px 20px rgba(0,0,0,0.3);
}
.song-card h4 { margin: 0 0 4px 0; color: #ffd32a; font-size: 17px; }
.song-card .artist { color: #a0a0a0; font-size: 13px; margin-bottom: 10px; }
.song-card .progression {
    font-family: 'Courier New', monospace;
    font-size: 18px;
    font-weight: 700;
    letter-spacing: 2px;
    color: #70a1ff;
}
.song-card .progression span {
    display: inline-block;
    background: rgba(112, 161, 255, 0.12);
    padding: 2px 10px;
    border-radius: 6px;
    margin: 2px 4px;
    cursor: pointer;
    transition: background 0.15s;
}
.song-card .progression span:hover {
    background: rgba(112, 161, 255, 0.3);
}

/* ===== Launchpad ===== */
#launchpad {
    margin: 28px 0 32px;
    padding: 22px;
    border-radius: 18px;
    background: linear-gradient(135deg, #101820, #1b2735);
    color: #f5f7fa;
    box-shadow: 0 18px 40px rgba(0,0,0,0.28);
}

.launchpad-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 16px;
    flex-wrap: wrap;
    margin-bottom: 10px;
}

.launchpad-title {
    margin: 0;
    font-size: 24px;
    color: #ffd32a;
}

.launchpad-subtitle {
    margin: 6px 0 0;
    color: #d7dce2;
    font-size: 14px;
}

.transport {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    align-items: center;
}

.transport label {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 14px;
}

.transport button,
.transport input {
    border: none;
    border-radius: 10px;
    padding: 10px 12px;
    font-size: 14px;
}

.transport button {
    background: #ffd32a;
    color: #111;
    font-weight: 700;
    cursor: pointer;
}

.transport button.secondary {
    background: #dfe6e9;
}

.transport button.recording {
    background: #ff6b6b;
    color: #fff;
}

.transport input {
    width: 72px;
    background: #f4f4f4;
    color: #111;
}

#launchpad-status {
    margin: 10px 0 16px;
    color: #9fd3ff;
    min-height: 20px;
    font-size: 14px;
}

.launchpad-grid {
    display: grid;
    grid-template-columns: 110px repeat(8, minmax(40px, 1fr));
    gap: 8px;
}

.lp-label,
.lp-step-label {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 42px;
    border-radius: 10px;
    background: rgba(255,255,255,0.06);
    font-weight: 700;
}

.lp-step-label {
    color: #9fd3ff;
    font-size: 13px;
}

.lp-label {
    justify-content: flex-start;
    padding-left: 12px;
    color: #f5f7fa;
}

.lp-cell {
    min-height: 42px;
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 10px;
    background: rgba(255,255,255,0.08);
    cursor: pointer;
    transition: transform 0.12s ease, background 0.12s ease, box-shadow 0.12s ease;
}

.lp-cell:hover {
    transform: translateY(-1px);
    background: rgba(255,255,255,0.14);
}

.lp-cell.active {
    background: linear-gradient(135deg, #1e90ff, #6c5ce7);
    box-shadow: 0 0 0 2px rgba(255,255,255,0.12) inset;
}

.lp-cell.playhead {
    outline: 2px solid #ffd32a;
    outline-offset: -2px;
}

@media (max-width: 900px) {
    .launchpad-grid {
        grid-template-columns: 88px repeat(8, minmax(28px, 1fr));
        gap: 6px;
    }

    .lp-label,
    .lp-step-label,
    .lp-cell {
        min-height: 36px;
        font-size: 12px;
    }
}
</style>

<!-- LEFT: Guitar chords -->
<div id="piano-zone"></div>

<div id="piano-sidebar"></div>

<!-- RIGHT: Drum pads -->
<div id="drum-zone"></div>

<div id="drum-sidebar">
    <button class="drum-key" data-drum="kick" onclick="playDrum('kick')">Kick</button>
    <button class="drum-key" data-drum="snare" onclick="playDrum('snare')">Snare</button>
    <button class="drum-key" data-drum="hihat" onclick="playDrum('hihat')">Hi-Hat</button>
    <button class="drum-key" data-drum="tom" onclick="playDrum('tom')">Tom</button>
    <button class="drum-key" data-drum="crash" onclick="playDrum('crash')">Crash</button>
    <button class="drum-key" data-drum="roll" onclick="playDrumRoll()">Roll</button>
</div>

<div id="chord-display"></div>
<div id="drum-display"></div>

Left edge -> Guitar chords | Right edge -> Drum kit

---

## Beat Lab

Build a quick groove, jam chords on top, or record a live take from the side pads.

<div id="launchpad">
    <div class="launchpad-header">
        <div>
            <h3 class="launchpad-title">Launchpad</h3>
            <p class="launchpad-subtitle">8-step sequencer for drums and chords. Live taps are recorded too.</p>
        </div>
        <div class="transport">
            <label for="key-select">Key
                <select id="key-select" onchange="changeKey(this.value)" style="border:none;border-radius:10px;padding:10px 12px;font-size:14px;background:#f4f4f4;color:#111;">
                    <option value="C">C Major</option>
                    <option value="G">G Major</option>
                    <option value="D">D Major</option>
                    <option value="A">A Major</option>
                    <option value="E">E Major</option>
                    <option value="F">F Major</option>
                    <option value="Bb">Bb Major</option>
                    <option value="Am">A Minor</option>
                    <option value="Em">E Minor</option>
                    <option value="Dm">D Minor</option>
                </select>
            </label>
            <label for="bpm-input"><input id="bpm-input" type="number" min="60" max="180" value="96"> <span style="font-size:12px;color:#aaa;">BPM</span></label>
            <label for="loops-input"><input id="loops-input" type="number" min="1" max="16" value="4"> <span style="font-size:12px;color:#aaa;">Loops</span></label>
            <button id="sequencer-toggle" onclick="toggleSequencer()">Play</button>
            <button class="secondary" onclick="stopSequencer()">Stop</button>
            <button class="secondary" onclick="clearPattern()">Clear</button>
            <button id="record-toggle" onclick="togglePerformanceRecording()">Record</button>
            <button class="secondary" onclick="playLiveTake()">Play Take</button>
            <button class="secondary" onclick="downloadBeat()" style="background:#2ed573;color:#fff;font-weight:700;">⬇ Download</button>
        </div>
    </div>
    <div id="launchpad-status">Click cells to program a groove. Use the side pads to overdub a live take.</div>
    <div class="launchpad-grid" id="launchpad-grid"></div>
</div>

<script>
let audioCtx = null;
let masterGain = null;

function getAudioCtx() {
    if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        masterGain = audioCtx.createGain();
        masterGain.connect(audioCtx.destination);
    }
    if (audioCtx.state === 'suspended') audioCtx.resume();
    return audioCtx;
}

const noteFreqs = {
    'C3':130.81,'C#3':138.59,'Db3':138.59,'D3':146.83,'D#3':155.56,'Eb3':155.56,
    'E3':164.81,'F3':174.61,'F#3':185.00,'Gb3':185.00,'G3':196.00,'G#3':207.65,
    'Ab3':207.65,'A3':220.00,'A#3':233.08,'Bb3':233.08,'B3':246.94,
    'C4':261.63,'C#4':277.18,'Db4':277.18,'D4':293.66,'D#4':311.13,'Eb4':311.13,
    'E4':329.63,'F4':349.23,'F#4':369.99,'Gb4':369.99,'G4':392.00,'G#4':415.30,
    'Ab4':415.30,'A4':440.00,'A#4':466.16,'Bb4':466.16,'B4':493.88,
    'C5':523.25,'D5':587.33,'E5':659.25
};

const chords = {
    'C':['C4','E4','G4'],'Cm':['C4','Eb4','G4'],
    'C#m':['C#4','E4','G#4'],
    'D':['D4','F#4','A4'],'Dm':['D4','F4','A4'],
    'Eb':['Eb4','G4','Bb4'],
    'E':['E4','G#4','B4'],'Em':['E4','G4','B4'],
    'F':['F3','A3','C4'],'F#m':['F#3','A3','C#4'],
    'G':['G3','B3','D4'],'Gm':['G3','Bb3','D4'],
    'G#m':['G#3','B3','D#4'],
    'A':['A3','C#4','E4'],'Am':['A3','C4','E4'],
    'Bb':['Bb3','D4','F4'],
    'B':['B3','D#4','F#4'],'Bm':['B3','D4','F#4']
};

const keyChords = {
    'C':['C','Dm','Em','F','G','Am'],
    'G':['G','Am','Bm','C','D','Em'],
    'D':['D','Em','F#m','G','A','Bm'],
    'A':['A','Bm','C#m','D','E','F#m'],
    'E':['E','F#m','G#m','A','B','C#m'],
    'F':['F','Gm','Am','Bb','C','Dm'],
    'Bb':['Bb','Cm','Dm','Eb','F','Gm'],
    'Am':['Am','C','Dm','Em','F','G'],
    'Em':['Em','G','Am','Bm','C','D'],
    'Dm':['Dm','F','Gm','Am','Bb','C']
};

const chordColorPalette = ['#ee5a24','#e67e22','#f0c419','#2ed573','#1e90ff','#6c5ce7'];

let currentKey = 'C';
const stepCount = 8;
const pattern = {};
let sequencerTimer = null;
let currentStep = 0;
let liveRecording = false;
let liveTake = [];
let recordStartTime = 0;

const drumIds = ['kick','snare','hihat','crash'];
drumIds.forEach(function(id) { pattern[id] = new Array(stepCount).fill(false); });

function initChordPatterns() {
    var names = keyChords[currentKey] || keyChords['C'];
    names.forEach(function(n) {
        if (!pattern[n]) pattern[n] = new Array(stepCount).fill(false);
    });
}
initChordPatterns();

function getLaunchpadTracks() {
    var drums = [
        {id:'kick',label:'Kick',type:'drum'},
        {id:'snare',label:'Snare',type:'drum'},
        {id:'hihat',label:'Hi-Hat',type:'drum'},
        {id:'crash',label:'Crash',type:'drum'}
    ];
    var names = keyChords[currentKey] || keyChords['C'];
    return drums.concat(names.map(function(n){ return {id:n,label:n,type:'chord'}; }));
}

function getChordColor(name) {
    var names = keyChords[currentKey] || keyChords['C'];
    var idx = names.indexOf(name);
    return idx >= 0 ? chordColorPalette[idx] : '#70a1ff';
}

function getKeyLabel(key) {
    var labels = {'C':'C Major','G':'G Major','D':'D Major','A':'A Major','E':'E Major',
        'F':'F Major','Bb':'Bb Major','Am':'A Minor','Em':'E Minor','Dm':'D Minor'};
    return labels[key] || key;
}

function playGuitarNoteToCtx(ctx, dest, freq, startTime) {
    var osc1 = ctx.createOscillator(), g1 = ctx.createGain();
    osc1.type = 'sawtooth'; osc1.frequency.value = freq;
    g1.gain.setValueAtTime(0.15, startTime);
    g1.gain.exponentialRampToValueAtTime(0.001, startTime + 0.08);
    osc1.connect(g1); g1.connect(dest);
    osc1.start(startTime); osc1.stop(startTime + 0.08);

    var osc2 = ctx.createOscillator(), g2 = ctx.createGain();
    osc2.type = 'triangle'; osc2.frequency.value = freq;
    g2.gain.setValueAtTime(0.12, startTime);
    g2.gain.setValueAtTime(0.12, startTime + 0.01);
    g2.gain.exponentialRampToValueAtTime(0.001, startTime + 1.2);
    osc2.connect(g2); g2.connect(dest);
    osc2.start(startTime); osc2.stop(startTime + 1.2);

    var osc3 = ctx.createOscillator(), g3 = ctx.createGain();
    osc3.type = 'sine'; osc3.frequency.value = freq * 2;
    g3.gain.setValueAtTime(0.04, startTime);
    g3.gain.exponentialRampToValueAtTime(0.001, startTime + 0.5);
    osc3.connect(g3); g3.connect(dest);
    osc3.start(startTime); osc3.stop(startTime + 0.5);

    var osc4 = ctx.createOscillator(), g4 = ctx.createGain();
    osc4.type = 'sine'; osc4.frequency.value = freq * 3;
    g4.gain.setValueAtTime(0.015, startTime);
    g4.gain.exponentialRampToValueAtTime(0.001, startTime + 0.25);
    osc4.connect(g4); g4.connect(dest);
    osc4.start(startTime); osc4.stop(startTime + 0.25);
}

function playChordToCtx(ctx, dest, chordName, time) {
    var notes = chords[chordName];
    if (!notes) return;
    notes.forEach(function(note, i) {
        playGuitarNoteToCtx(ctx, dest, noteFreqs[note], time + i * 0.025);
    });
}

function playDrumToCtx(ctx, dest, type, time) {
    if (type === 'kick') {
        var osc = ctx.createOscillator(), g = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(150, time);
        osc.frequency.exponentialRampToValueAtTime(40, time + 0.12);
        g.gain.setValueAtTime(0.8, time);
        g.gain.exponentialRampToValueAtTime(0.001, time + 0.4);
        osc.connect(g); g.connect(dest);
        osc.start(time); osc.stop(time + 0.4);
    } else if (type === 'snare') {
        var bufSize = ctx.sampleRate * 0.15;
        var buf = ctx.createBuffer(1, bufSize, ctx.sampleRate);
        var data = buf.getChannelData(0);
        for (var i = 0; i < bufSize; i++) data[i] = Math.random() * 2 - 1;
        var noise = ctx.createBufferSource(); noise.buffer = buf;
        var nGain = ctx.createGain();
        nGain.gain.setValueAtTime(0.5, time);
        nGain.gain.exponentialRampToValueAtTime(0.001, time + 0.15);
        var filter = ctx.createBiquadFilter();
        filter.type = 'bandpass'; filter.frequency.value = 3000;
        noise.connect(filter); filter.connect(nGain); nGain.connect(dest);
        noise.start(time);
        var osc2 = ctx.createOscillator(), g2 = ctx.createGain();
        osc2.type = 'triangle'; osc2.frequency.value = 180;
        g2.gain.setValueAtTime(0.35, time);
        g2.gain.exponentialRampToValueAtTime(0.001, time + 0.08);
        osc2.connect(g2); g2.connect(dest);
        osc2.start(time); osc2.stop(time + 0.08);
    } else if (type === 'hihat') {
        var bufSize = ctx.sampleRate * 0.06;
        var buf = ctx.createBuffer(1, bufSize, ctx.sampleRate);
        var data = buf.getChannelData(0);
        for (var i = 0; i < bufSize; i++) data[i] = Math.random() * 2 - 1;
        var noise = ctx.createBufferSource(); noise.buffer = buf;
        var filter = ctx.createBiquadFilter();
        filter.type = 'highpass'; filter.frequency.value = 7000;
        var g = ctx.createGain();
        g.gain.setValueAtTime(0.3, time);
        g.gain.exponentialRampToValueAtTime(0.001, time + 0.06);
        noise.connect(filter); filter.connect(g); g.connect(dest);
        noise.start(time);
    } else if (type === 'tom') {
        var osc = ctx.createOscillator(), g = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(120, time);
        osc.frequency.exponentialRampToValueAtTime(70, time + 0.2);
        g.gain.setValueAtTime(0.6, time);
        g.gain.exponentialRampToValueAtTime(0.001, time + 0.35);
        osc.connect(g); g.connect(dest);
        osc.start(time); osc.stop(time + 0.35);
    } else if (type === 'crash') {
        var bufSize = ctx.sampleRate * 0.8;
        var buf = ctx.createBuffer(1, bufSize, ctx.sampleRate);
        var data = buf.getChannelData(0);
        for (var i = 0; i < bufSize; i++) data[i] = Math.random() * 2 - 1;
        var noise = ctx.createBufferSource(); noise.buffer = buf;
        var filter = ctx.createBiquadFilter();
        filter.type = 'highpass'; filter.frequency.value = 4000;
        var g = ctx.createGain();
        g.gain.setValueAtTime(0.35, time);
        g.gain.exponentialRampToValueAtTime(0.001, time + 0.8);
        noise.connect(filter); filter.connect(g); g.connect(dest);
        noise.start(time);
    }
}

function playChord(chordName) {
    var ctx = getAudioCtx();
    playChordToCtx(ctx, masterGain, chordName, ctx.currentTime);

    recordHit('chord', chordName);

    var btn = document.querySelector('.piano-key[data-chord="' + chordName + '"]');
    if (btn) {
        btn.classList.add('playing');
        setTimeout(function() { btn.classList.remove('playing'); }, 200);
    }

    var display = document.getElementById('chord-display');
    display.textContent = chordName;
    display.style.color = getChordColor(chordName);
    display.classList.add('show');
    setTimeout(function() { display.classList.remove('show'); }, 800);
}

function playDrum(type) {
    var ctx = getAudioCtx();
    playDrumToCtx(ctx, masterGain, type, ctx.currentTime);
    recordHit('drum', type);

    var btn = document.querySelector('.drum-key[data-drum="' + type + '"]');
    if (btn) {
        btn.classList.add('playing');
        setTimeout(function() { btn.classList.remove('playing'); }, 150);
    }

    var dd = document.getElementById('drum-display');
    var labels = { kick: '💥 Kick', snare: '🪘 Snare', hihat: '🎩 Hi-Hat', tom: '🔊 Tom', crash: '💫 Crash' };
    dd.textContent = labels[type] || type;
    dd.classList.add('show');
    setTimeout(function() { dd.classList.remove('show'); }, 500);
}

function playDrumRoll() {
    var count = 12;
    for (var i = 0; i < count; i++) {
        (function(idx) {
            setTimeout(function() { playDrum('snare'); }, idx * 60);
        })(i);
    }
    var dd = document.getElementById('drum-display');
    dd.textContent = '🥁 DRUM ROLL!';
    dd.classList.add('show');
    setTimeout(function() { dd.classList.remove('show'); }, 1000);
}

function buildSidebar() {
    var sidebar = document.getElementById('piano-sidebar');
    if (!sidebar) return;
    sidebar.innerHTML = '';
    var names = keyChords[currentKey] || keyChords['C'];
    names.forEach(function(name) {
        var btn = document.createElement('button');
        btn.className = 'piano-key';
        btn.dataset.chord = name;
        btn.textContent = name;
        btn.onclick = function() { playChord(name); };
        sidebar.appendChild(btn);
    });
}

function changeKey(newKey) {
    stopSequencer();
    currentKey = newKey;
    Object.keys(pattern).forEach(function(id) {
        if (drumIds.indexOf(id) < 0) delete pattern[id];
    });
    initChordPatterns();
    buildSidebar();
    buildLaunchpad();
    setLaunchpadStatus('Key changed to ' + getKeyLabel(newKey));
}

function setLaunchpadStatus(message) {
    var status = document.getElementById('launchpad-status');
    if (status) status.textContent = message;
}

function buildLaunchpad() {
    var grid = document.getElementById('launchpad-grid');
    if (!grid) return;
    grid.innerHTML = '';

    var spacer = document.createElement('div');
    spacer.className = 'lp-step-label';
    spacer.textContent = 'Track';
    grid.appendChild(spacer);

    for (var step = 0; step < stepCount; step++) {
        var stepLabel = document.createElement('div');
        stepLabel.className = 'lp-step-label';
        stepLabel.textContent = String(step + 1);
        grid.appendChild(stepLabel);
    }

    var tracks = getLaunchpadTracks();
    tracks.forEach(function(track) {
        var label = document.createElement('div');
        label.className = 'lp-label';
        label.textContent = track.label;
        grid.appendChild(label);

        for (var stepIndex = 0; stepIndex < stepCount; stepIndex++) {
            (function(trackId, currentIndex) {
                var cell = document.createElement('button');
                cell.type = 'button';
                cell.className = 'lp-cell';
                cell.dataset.track = trackId;
                cell.dataset.step = String(currentIndex);
                if (pattern[trackId] && pattern[trackId][currentIndex]) cell.classList.add('active');
                cell.onclick = function() {
                    if (!pattern[trackId]) pattern[trackId] = new Array(stepCount).fill(false);
                    pattern[trackId][currentIndex] = !pattern[trackId][currentIndex];
                    cell.classList.toggle('active', pattern[trackId][currentIndex]);
                    if (pattern[trackId][currentIndex]) triggerTrack(trackId);
                };
                grid.appendChild(cell);
            })(track.id, stepIndex);
        }
    });
}

function updatePlayhead(step) {
    var cells = document.querySelectorAll('.lp-cell');
    cells.forEach(function(cell) {
        cell.classList.toggle('playhead', Number(cell.dataset.step) === step);
    });
}

function clearPlayhead() {
    var cells = document.querySelectorAll('.lp-cell');
    cells.forEach(function(cell) {
        cell.classList.remove('playhead');
    });
}

function triggerTrack(trackId) {
    if (drumIds.indexOf(trackId) >= 0) playDrum(trackId);
    else playChord(trackId);
}

function getStepDurationMs() {
    var bpmInput = document.getElementById('bpm-input');
    var bpm = bpmInput ? Number(bpmInput.value) : 96;
    if (!bpm || bpm < 60) bpm = 60;
    if (bpm > 180) bpm = 180;
    if (bpmInput) bpmInput.value = bpm;
    return (60 / bpm) * 1000 / 2;
}

function runSequencerStep() {
    var tracks = getLaunchpadTracks();
    tracks.forEach(function(track) {
        if (pattern[track.id] && pattern[track.id][currentStep]) {
            triggerTrack(track.id);
        }
    });

    updatePlayhead(currentStep);
    currentStep = (currentStep + 1) % stepCount;
}

function toggleSequencer() {
    getAudioCtx();

    if (sequencerTimer) {
        stopSequencer();
        return;
    }

    currentStep = 0;
    runSequencerStep();
    sequencerTimer = setInterval(runSequencerStep, getStepDurationMs());

    var toggleButton = document.getElementById('sequencer-toggle');
    if (toggleButton) toggleButton.textContent = 'Pause';
    setLaunchpadStatus('Sequencer running. Change BPM anytime or tap the side pads to layer a live take.');
}

function stopSequencer() {
    if (sequencerTimer) {
        clearInterval(sequencerTimer);
        sequencerTimer = null;
    }

    clearPlayhead();
    currentStep = 0;

    var toggleButton = document.getElementById('sequencer-toggle');
    if (toggleButton) toggleButton.textContent = 'Play';
    setLaunchpadStatus('Sequencer stopped.');
}

function clearPattern() {
    var tracks = getLaunchpadTracks();
    tracks.forEach(function(track) {
        pattern[track.id] = new Array(stepCount).fill(false);
    });

    var cells = document.querySelectorAll('.lp-cell');
    cells.forEach(function(cell) {
        cell.classList.remove('active', 'playhead');
    });

    currentStep = 0;
    setLaunchpadStatus('Pattern cleared.');
}

function recordHit(kind, value) {
    if (!liveRecording) return;
    liveTake.push({
        kind: kind,
        value: value,
        at: performance.now() - recordStartTime
    });
}

function togglePerformanceRecording() {
    var recordButton = document.getElementById('record-toggle');
    getAudioCtx();

    if (!liveRecording) {
        liveTake = [];
        liveRecording = true;
        recordStartTime = performance.now();
        if (recordButton) {
            recordButton.textContent = 'Stop Rec';
            recordButton.classList.add('recording');
        }
        setLaunchpadStatus('Recording live taps from the side pads and launchpad playback.');
        return;
    }

    liveRecording = false;
    if (recordButton) {
        recordButton.textContent = 'Record';
        recordButton.classList.remove('recording');
    }
    setLaunchpadStatus('Recorded ' + liveTake.length + ' events. Use Play Take to hear it back.');
}

function playLiveTake() {
    if (!liveTake.length) {
        setLaunchpadStatus('No live take recorded yet. Press Record and tap the side pads first.');
        return;
    }

    getAudioCtx();
    setLaunchpadStatus('Playing back your recorded take.');

    liveTake.forEach(function(event) {
        setTimeout(function() {
            if (event.kind === 'drum') playDrum(event.value);
            if (event.kind === 'chord') playChord(event.value);
        }, event.at);
    });
}

function downloadBeat() {
    var tracks = getLaunchpadTracks();
    var hasNotes = false;
    tracks.forEach(function(t) {
        if (pattern[t.id]) pattern[t.id].forEach(function(v) { if (v) hasNotes = true; });
    });
    if (!hasNotes) { setLaunchpadStatus('Nothing to download — program a pattern first.'); return; }

    var bpmInp = document.getElementById('bpm-input');
    var bpm = bpmInp ? Number(bpmInp.value) : 96;
    if (!bpm || bpm < 60) bpm = 60; if (bpm > 180) bpm = 180;
    var stepSec = (60 / bpm) / 2;
    var loopsInp = document.getElementById('loops-input');
    var loops = loopsInp ? Number(loopsInp.value) : 4;
    if (!loops || loops < 1) loops = 1; if (loops > 16) loops = 16;
    var oneLoopSec = stepCount * stepSec;
    var totalSec = oneLoopSec * loops + 1.5;
    var sampleRate = 44100;
    var totalSamples = Math.ceil(totalSec * sampleRate);
    var offCtx = new OfflineAudioContext(2, totalSamples, sampleRate);

    for (var loop = 0; loop < loops; loop++) {
        for (var step = 0; step < stepCount; step++) {
            var t = loop * oneLoopSec + step * stepSec;
            tracks.forEach(function(track) {
                if (pattern[track.id] && pattern[track.id][step]) {
                    if (track.type === 'drum') playDrumToCtx(offCtx, offCtx.destination, track.id, t);
                    else playChordToCtx(offCtx, offCtx.destination, track.id, t);
                }
            });
        }
    }

    setLaunchpadStatus('Rendering beat…');
    offCtx.startRendering().then(function(buffer) {
        var wav = audioBufferToWav(buffer);
        var blob = new Blob([wav], { type: 'audio/wav' });
        var url = URL.createObjectURL(blob);
        var a = document.createElement('a');
        a.href = url;
        a.download = 'beat-' + currentKey + '-' + bpm + 'bpm.wav';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
        setLaunchpadStatus('Beat downloaded!');
    });
}

function writeString(view, offset, str) {
    for (var i = 0; i < str.length; i++) view.setUint8(offset + i, str.charCodeAt(i));
}

function audioBufferToWav(buffer) {
    var numCh = buffer.numberOfChannels, sr = buffer.sampleRate, bps = 16;
    var blockAlign = numCh * (bps / 8);
    var dataSize = buffer.length * blockAlign;
    var arrBuf = new ArrayBuffer(44 + dataSize);
    var v = new DataView(arrBuf);
    writeString(v, 0, 'RIFF');
    v.setUint32(4, 36 + dataSize, true);
    writeString(v, 8, 'WAVE');
    writeString(v, 12, 'fmt ');
    v.setUint32(16, 16, true);
    v.setUint16(20, 1, true);
    v.setUint16(22, numCh, true);
    v.setUint32(24, sr, true);
    v.setUint32(28, sr * blockAlign, true);
    v.setUint16(32, blockAlign, true);
    v.setUint16(34, bps, true);
    writeString(v, 36, 'data');
    v.setUint32(40, dataSize, true);
    var channels = [];
    for (var ch = 0; ch < numCh; ch++) channels.push(buffer.getChannelData(ch));
    var off = 44;
    for (var i = 0; i < buffer.length; i++) {
        for (var ch = 0; ch < numCh; ch++) {
            var s = Math.max(-1, Math.min(1, channels[ch][i]));
            s = s < 0 ? s * 0x8000 : s * 0x7FFF;
            v.setInt16(off, s, true);
            off += 2;
        }
    }
    return arrBuf;
}

buildSidebar();
buildLaunchpad();
</script>
