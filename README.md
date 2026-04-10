<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LogicLeap: Protocol 404</title>
    <style>
        :root {
            --neon: #39ff14;
            --bg: #050505;
            --panel: #111;
        }

        body {
            background-color: var(--bg);
            color: var(--neon);
            font-family: 'Courier New', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        #terminal {
            width: 90%;
            max-width: 600px;
            background: var(--panel);
            border: 2px solid var(--neon);
            padding: 30px;
            box-shadow: 0 0 20px rgba(57, 255, 20, 0.1);
            position: relative;
        }

        .persistence-tab {
            position: absolute;
            top: -40px;
            right: 0;
            background: #ff4b2b;
            color: white;
            padding: 5px 15px;
            font-size: 12px;
            cursor: pointer;
            border: none;
            font-weight: bold;
        }

        .screen { display: none; }
        .active { display: block; }

        h2 { border-bottom: 1px solid var(--neon); padding-bottom: 10px; font-size: 1.2rem; }
        
        .code-block {
            background: #000;
            padding: 15px;
            margin: 15px 0;
            border-left: 3px solid var(--neon);
            font-size: 0.9rem;
            line-height: 1.4;
        }

        .options-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
            margin-top: 20px;
        }

        button.opt {
            background: transparent;
            color: var(--neon);
            border: 1px solid var(--neon);
            padding: 12px;
            text-align: left;
            cursor: pointer;
            transition: 0.2s;
        }

        button.opt:hover {
            background: var(--neon);
            color: black;
        }

        .status-bar {
            margin-top: 20px;
            font-size: 10px;
            text-transform: uppercase;
            letter-spacing: 2px;
            opacity: 0.7;
        }

        /* Glitch Effect on Wrong Answer */
        .glitch { animation: shake 0.2s linear 3; border-color: red !important; }
        @keyframes shake {
            0% { transform: translate(5px); }
            50% { transform: translate(-5px); }
            100% { transform: translate(0); }
        }
    </style>
</head>
<body>

    <div id="terminal">
        <button class="persistence-tab" onclick="location.reload()">[RESTART_SESSION]</button>
        
        <div id="room1" class="screen active">
            <h2>LEVEL_01: DECOMPOSITION</h2>
            <p>SYSTEM CRASH: "School Fundraiser" is too large to process.</p>
            <div class="code-block">
                Identify the sub-tasks for the <strong>"Decorations"</strong> module:
            </div>
            <div class="options-grid">
                <button class="opt" onclick="wrong(1)">A) Buy Pizza and Napkins</button>
                <button class="opt" onclick="next(1, 2)">B) Paint Banners and Hang Lights</button>
                <button class="opt" onclick="wrong(1)">C) Hire a DJ and Test Speakers</button>
            </div>
        </div>

        <div id="room2" class="screen">
            <h2>LEVEL_02: PATTERN_RECOGNITION</h2>
            <p>ANALYZING HISTORICAL LOGS...</p>
            <div class="code-block">
                LOG_2024: 100 students showed up.<br>
                LOG_2025: 150 students showed up.<br>
                LOG_2026: 225 students showed up.
            </div>
            <div class="options-grid">
                <button class="opt" onclick="next(2, 3)">A) Attendance is increasing by 50% each year.</button>
                <button class="opt" onclick="wrong(2)">B) Attendance is staying the same.</button>
                <button class="opt" onclick="wrong(2)">C) Attendance is decreasing.</button>
            </div>
        </div>

        <div id="room3" class="screen">
            <h2>LEVEL_03: ABSTRACTION</h2>
            <p>FILTERING SYSTEM "FLUFF"...</p>
            <div class="code-block">
                DATA: "The fundraiser is on Friday. The sky is blue. The budget is $500. The principal owns a cat."
            </div>
            <p>What is the Crucial Information?</p>
            <div class="options-grid">
                <button class="opt" onclick="wrong(3)">A) The cat and the blue sky.</button>
                <button class="opt" onclick="next(3, 4)">B) Friday / $500 Budget.</button>
                <button class="opt" onclick="wrong(3)">C) All data is equally important.</button>
            </div>
        </div>

        <div id="room4" class="screen">
            <h2>LEVEL_04: ALGORITHMIC_DESIGN</h2>
            <p>CREATING THE "RECIPE"...</p>
            <div class="code-block">
                1. Unlock Door <br>
                2. Set up Tables <br>
                3. Start Music
            </div>
            <p>Is this a valid Algorithm?</p>
            <div class="options-grid">
                <button class="opt" onclick="next(4, 5)">A) Yes: It is a logical, step-by-step sequence.</button>
                <button class="opt" onclick="wrong(4)">B) No: It has no ending.</button>
            </div>
        </div>

        <div id="room5" class="screen">
            <h2>LEVEL_05: THE_DEBUGGER_FINAL</h2>
            <p>IDENTIFY THE BUG TYPE:</p>
            <div class="code-block" id="debug-code">
                console.log(Welcome to Class);
            </div>
            <div class="options-grid" id="debug-options">
                <button class="opt" onclick="checkDebug('Syntax')">Syntax Error</button>
                <button class="opt" onclick="checkDebug('Name')">Name Error</button>
                <button class="opt" onclick="checkDebug('Type')">Type Error</button>
                <button class="opt" onclick="checkDebug('Logic')">Logic Error</button>
            </div>
        </div>

        <div id="win" class="screen">
            <h2>PROTOCOL_404_CLEARED</h2>
            <div class="code-block">
                > System Restored.<br>
                > LogicLeap status: COMPLETED.<br>
                > Great work, Admin.
            </div>
        </div>

        <div class="status-bar" id="status">Pillar: Decomposition | Level: 01</div>
    </div>

    <script>
        let debugStep = 0;
        const debugTasks = [
            { code: 'console.log(Welcome to Class);', ans: 'Syntax' },
            { code: 'var name = "Adam"; log(usr);', ans: 'Name' },
            { code: 'var total = 10 + "5";', ans: 'Type' },
            { code: 'if (x = 5) { }', ans: 'Logic' }
        ];

        const pillars = ["Decomposition", "Pattern Recognition", "Abstraction", "Algorithmic Design", "Debugging"];

        function next(current, next) {
            document.getElementById('room' + current).classList.remove('active');
            document.getElementById('room' + next).classList.add('active');
            document.getElementById('status').innerText = `Pillar: ${pillars[next-1]} | Level: 0${next}`;
        }

        function wrong(room) {
            const term = document.getElementById('terminal');
            term.classList.add('glitch');
            setTimeout(() => term.classList.remove('glitch'), 500);
        }

        function checkDebug(choice) {
            if (choice === debugTasks[debugStep].ans) {
                debugStep++;
                if (debugStep < debugTasks.length) {
                    document.getElementById('debug-code').innerText = debugTasks[debugStep].code;
                } else {
                    document.getElementById('room5').classList.remove('active');
                    document.getElementById('win').classList.add('active');
                }
            } else {
                wrong(5);
            }
        }
    </script>
</body>
</html>
