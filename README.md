<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Public Health Crisis | Executive Simulation</title>
  <style>
    :root {
      --navy: #14263e;
      --blue: #245c85;
      --teal: #087e80;
      --light: #f3f6fa;
      --line: #dbe3ec;
      --ink: #243247;
      --red: #a72d36;
      --gold: #e3a536;
      --white: #ffffff;
      --muted: #526176;
      --panel-bg: #ffffff;
      --soft-blue: #eef6fa;
      --soft-teal: #e9f6f4;
      --soft-red: #fff2f1;
      --shadow: rgba(16, 24, 40, 0.06);
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: var(--light);
      color: var(--ink);
      line-height: 1.55;
    }

    header {
      background: var(--navy);
      color: var(--white);
      padding: 28px max(20px, calc((100% - 1100px) / 2));
      box-shadow: 0 2px 10px rgba(20, 38, 62, 0.15);
    }

    header h1 {
      margin: 0;
      font-size: clamp(1.6rem, 2vw, 2.1rem);
      letter-spacing: 0.02em;
    }

    header p {
      margin: 6px 0 0;
      color: #dce6f2;
    }

    main {
      max-width: 1100px;
      margin: 25px auto;
      padding: 0 18px 40px;
    }

    .panel {
      background: var(--panel-bg);
      border: 1px solid var(--line);
      border-radius: 12px;
      padding: 24px;
      margin-bottom: 18px;
      box-shadow: 0 3px 12px var(--shadow);
    }

    h2 {
      margin-top: 0;
      color: var(--navy);
      font-size: clamp(1.4rem, 2vw, 1.8rem);
    }

    h3 {
      color: var(--navy);
      margin-top: 1.3rem;
    }

    p {
      margin-top: 0;
    }

    button,
    input,
    textarea,
    select {
      font: inherit;
    }

    button {
      cursor: pointer;
      border-radius: 7px;
      border: 1px solid var(--blue);
      background: var(--blue);
      color: var(--white);
      padding: 11px 17px;
      margin: 5px 5px 5px 0;
      transition: filter 0.2s ease, transform 0.2s ease;
    }

    button:hover {
      filter: brightness(0.95);
    }

    button:active {
      transform: translateY(1px);
    }

    button.secondary {
      background: var(--white);
      color: var(--blue);
    }

    button:disabled {
      opacity: 0.55;
      cursor: not-allowed;
    }

    button:focus-visible,
    input:focus-visible,
    textarea:focus-visible,
    select:focus-visible {
      outline: 3px solid var(--gold);
      outline-offset: 2px;
    }

    .hidden {
      display: none !important;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
      gap: 12px;
    }

    .metric {
      background: #f4f8fb;
      padding: 14px;
      border-radius: 9px;
      border: 1px solid var(--line);
    }

    .metric strong {
      display: block;
      font-size: 1.4rem;
      margin-bottom: 3px;
    }

    .metric small {
      display: block;
      color: var(--muted);
    }

    .track {
      height: 9px;
      background: #dce5ed;
      border-radius: 10px;
      overflow: hidden;
      margin-top: 9px;
    }

    .fill {
      height: 100%;
      background: var(--teal);
      transition: width 0.35s ease;
      border-radius: 10px;
    }

    .option {
      display: block;
      width: 100%;
      text-align: left;
      margin: 9px 0;
      background: var(--white);
      color: var(--ink);
      border: 2px solid var(--line);
      padding: 16px;
    }

    .option:hover {
      background: var(--soft-blue);
    }

    .option.selected {
      border-color: var(--teal);
      background: var(--soft-teal);
    }

    .option strong {
      display: block;
      font-size: 1.02rem;
    }

    .option span {
      display: block;
      font-size: 0.94rem;
      margin-top: 6px;
      color: #394b60;
    }

    textarea,
    input,
    select {
      width: 100%;
      padding: 12px;
      border: 1px solid #9cabbc;
      border-radius: 7px;
      margin: 7px 0 13px;
      background: var(--white);
      color: var(--ink);
    }

    textarea {
      min-height: 105px;
      resize: vertical;
    }

    label {
      display: block;
      font-weight: bold;
      margin-top: 0.7rem;
    }

    .callout {
      border-left: 5px solid var(--teal);
      background: #eff8f7;
      padding: 15px;
      margin: 16px 0;
      border-radius: 0 8px 8px 0;
      white-space: pre-line;
    }

    .warning {
      border-left-color: var(--red);
      background: var(--soft-red);
    }

    .role {
      display: inline-block;
      background: #e9edf4;
      color: var(--navy);
      padding: 4px 10px;
      border-radius: 15px;
      font-size: 0.83rem;
      font-weight: bold;
      margin-bottom: 8px;
      letter-spacing: 0.04em;
      text-transform: uppercase;
    }

    .progress {
      height: 9px;
      background: #dce5ed;
      border-radius: 10px;
      overflow: hidden;
      margin-top: 10px;
    }

    .progress div {
      height: 100%;
      background: var(--teal);
      transition: width 0.3s ease;
    }

    .topline {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;
    }

    #timer {
      font-weight: bold;
      font-size: 1.2rem;
    }

    #timer.late {
      color: var(--red);
    }

    #validation {
      min-height: 1.2rem;
      color: var(--red);
      font-weight: 600;
      margin-top: 0.5rem;
    }

    .meta-row {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 10px;
      align-items: center;
      margin-bottom: 8px;
    }

    footer {
      text-align: center;
      padding: 16px 20px 30px;
      color: var(--muted);
      font-size: 0.95rem;
    }

    @media (max-width: 600px) {
      .panel {
        padding: 17px;
      }

      header h1 {
        font-size: 1.4rem;
      }

      .topline,
      .meta-row {
        flex-direction: column;
        align-items: flex-start;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Public Health Crisis</h1>
    <p>Executive Leadership Decision Simulation</p>
  </header>

  <main>
    <section id="intro" class="panel">
      <span class="role">Confidential executive briefing</span>
      <h2>Welcome to Redwood Valley</h2>
      <p>
        You are the executive leadership team responsible for coordinating a response to an escalating infectious disease emergency in fictional Redwood Valley.
      </p>
      <p>
        The region has approximately 240,000 residents, two hospitals, and a county public health department. A suspected measles outbreak has emerged following several large community gatherings.
      </p>
      <div class="callout">
        <strong>Your mission:</strong>
        Protect public health while navigating legal authority, patient rights, organizational constraints, equity, political pressure, and community trust.
      </div>
      <p>
        There is no single perfect solution. Your team must defend its choices and consider their consequences.
      </p>

      <label for="team">Executive team name</label>
      <input id="team" placeholder="Example: Team Redwood" />
      <button id="start" type="button">Begin Simulation</button>
    </section>

    <div id="game" class="hidden">
      <section class="panel">
        <div class="topline">
          <strong id="roundLabel">Round 1 of 5</strong>
          <span id="timer" role="timer" aria-live="polite">45:00</span>
        </div>
        <div class="progress" aria-label="Simulation progress">
          <div id="progressFill" style="width: 20%;"></div>
        </div>
        <p id="phaseLabel"></p>
        <button class="secondary" id="pauseBtn" type="button">Pause Timer</button>
      </section>

      <section class="panel">
        <h2>Crisis Dashboard</h2>
        <p>
          These indicators are fictional teaching estimates, not epidemiological predictions or legal scores.
        </p>
        <div id="dashboard" class="grid"></div>
      </section>

      <section id="decisionPanel" class="panel">
        <span id="roundRole" class="role"></span>
        <h2 id="roundTitle"></h2>
        <p id="story"></p>
        <div id="context" class="callout"></div>
        <h3>Executive decision</h3>
        <p id="question"></p>
        <div id="options"></div>

        <div id="customBox" class="hidden">
          <label for="customPolicy">Your proposed policy</label>
          <textarea id="customPolicy" placeholder="Describe your alternative or blended strategy."></textarea>

          <label for="customStrategy">Which approach best describes your proposal?</label>
          <select id="customStrategy">
            <option value="0">Protective / precautionary</option>
            <option value="1">Balanced / targeted</option>
            <option value="2">Minimal intervention / voluntary</option>
          </select>
        </div>

        <label for="reasoning">Explain your team's legal and ethical reasoning</label>
        <textarea id="reasoning" placeholder="What authority applies? Who is affected? What tradeoffs are you accepting?"></textarea>

        <button id="submitDecision" type="button">Submit Executive Decision</button>
        <p id="validation" role="alert" aria-live="polite"></p>
      </section>

      <section id="resultPanel" class="panel hidden" aria-live="polite">
        <span class="role">Consequence briefing</span>
        <h2>Immediate consequences</h2>
        <p id="resultText"></p>

        <h3>Stakeholder response</h3>
        <div id="stakeholder" class="callout"></div>

        <h3>Legal and ethical considerations</h3>
        <p id="legalText"></p>

        <p><strong>Executive reflection:</strong> <span id="reflection"></span></p>
        <button id="next" type="button">Continue to Next Round</button>
      </section>
    </div>

    <section id="ending" class="panel hidden">
      <span class="role">After-action review</span>
      <h2>Simulation complete</h2>
      <p id="finalNarrative"></p>
      <div id="finalDashboard" class="grid"></div>

      <h3>Leadership debrief</h3>
      <ol>
        <li>Which decision presented the greatest conflict between public safety and individual rights?</li>
        <li>Where did hospital authority end and public health authority begin?</li>
        <li>Which groups experienced disproportionate burdens?</li>
        <li>How did your communication choices affect trust?</li>
        <li>What would you change with better information?</li>
        <li>What safeguards would you require before implementing your most restrictive policy?</li>
      </ol>

      <label for="finalReflection">Final team reflection</label>
      <textarea id="finalReflection" placeholder="Summarize your most important leadership lessons."></textarea>
      <button id="download" type="button">Download Decision Record</button>
      <button class="secondary" id="restart" type="button">Restart Simulation</button>
    </section>
  </main>

  <footer>
    Fictional educational simulation. Not medical or legal advice.
  </footer>

  <script>
    "use strict";

    const metricMeta = {
      severity: "Outbreak severity",
      trust: "Community trust",
      capacity: "Hospital capacity",
      legal: "Legal exposure",
      pressure: "Political pressure",
      equity: "Equity impact",
      morale: "Staff morale"
    };

    const rounds = [
      {
        title: "First Alert",
        role: "County Health Director",
        story:
          "Redwood Valley confirms 12 measles cases. Several patients visited schools, a crowded community event, and a hospital emergency department while potentially infectious. Vaccination coverage varies substantially across neighborhoods.",
        context:
          "The hospital can manage its facilities and clinical operations. The county health department must separately assess its statutory authority for public health orders.",
        question: "How should your leadership team respond during the first 24 hours?",
        options: [
          {
            title: "Launch a broad emergency response",
            detail: "Public warning, rapid tracing, expanded testing and vaccination access.",
            result: "Response capacity expands quickly, but some residents question the urgency.",
            stakeholder: "The mayor asks whether the public announcement could create unnecessary panic.",
            legal: "Emergency messaging and resource mobilization do not automatically authorize compulsory restrictions.",
            reflection: "How would you explain the level of uncertainty to the public?",
            effects: { severity: -9, trust: -3, capacity: -6, legal: 3, pressure: 9, equity: 4, morale: -3 }
          },
          {
            title: "Use a targeted, coordinated response",
            detail: "Notify affected groups, coordinate clinical response, and expand voluntary services.",
            result: "Targeted action reduces disruption, although some exposures remain unidentified.",
            stakeholder: "A school principal asks why families outside the identified exposure network have not been notified.",
            legal: "Targeting should rely on evidence, consistent criteria, and equitable access.",
            reflection: "What evidence would justify expanding the response?",
            effects: { severity: -5, trust: 5, capacity: -3, legal: -3, pressure: 2, equity: 4, morale: 2 }
          },
          {
            title: "Begin with voluntary monitoring",
            detail: "Issue limited guidance and rely on healthcare providers to report new cases.",
            result: "Initial disruption is limited, but additional exposures go undetected.",
            stakeholder: "Emergency clinicians report concern that the response is too slow.",
            legal: "Avoiding restrictions reduces some liberty concerns but does not eliminate institutional duties to respond.",
            reflection: "What is the ethical cost of delay?",
            effects: { severity: 13, trust: 1, capacity: -8, legal: 5, pressure: 6, equity: -6, morale: -7 }
          }
        ]
      },
      {
        title: "Isolation Dispute",
        role: "Hospital Legal Counsel",
        story:
          "A patient with suspected measles refuses recommended isolation and wishes to leave the hospital. Several exposed individuals have also declined voluntary guidance.",
        context:
          "Legal counsel cautions that clinical recommendations, hospital infection-control policies, and government isolation orders involve different sources of authority.",
        question: "How will your team respond to the patient and the broader exposure risk?",
        options: [
          {
            title: "Seek a formal isolation order",
            detail: "Request public health legal review and pursue compulsory measures if authorized.",
            result: "Transmission risk is reduced, but the intervention attracts scrutiny.",
            stakeholder: "A patient advocate demands information about appeal rights, humane conditions, and access to counsel.",
            legal: "Authority, procedural safeguards, necessity, and least-restrictive alternatives must be assessed under applicable law.",
            reflection: "What procedural protections would make this intervention defensible?",
            effects: { severity: -11, trust: -9, capacity: -3, legal: 12, pressure: 10, equity: -7, morale: -2 }
          },
          {
            title: "Negotiate supported voluntary isolation",
            detail: "Offer clear information, assistance, and a defined reassessment process.",
            result: "Most individuals cooperate, but some exposure risk persists.",
            stakeholder: "A social worker requests transportation, food, and income support for affected households.",
            legal: "Voluntary compliance may be more sustainable when meaningful supports address practical barriers.",
            reflection: "What happens if voluntary cooperation fails?",
            effects: { severity: -5, trust: 9, capacity: -5, legal: -5, pressure: -2, equity: 9, morale: 2 }
          },
          {
            title: "Avoid compulsory measures",
            detail: "Provide advice and allow individuals to determine whether to comply.",
            result: "Individual autonomy is preserved, but additional contacts are exposed.",
            stakeholder: "A parent of an immunocompromised child argues that the response ignores vulnerable residents.",
            legal: "Respect for autonomy must be balanced against foreseeable harms to others.",
            reflection: "When might nonintervention become ethically unacceptable?",
            effects: { severity: 15, trust: -5, capacity: -8, legal: 7, pressure: 9, equity: -10, morale: -5 }
          }
        ]
      },
      {
        title: "Workforce Shortage",
        role: "Hospital Chief Operating Officer",
        story:
          "Hospital admissions are increasing. Several staff members have been exposed, and others are requesting leave. The emergency department is approaching its operational limits.",
        context:
          "The hospital must address patient safety, employment obligations, infection control, disability-related accommodations, and equitable access to services.",
        question: "What workforce and service strategy will your team adopt?",
        options: [
          {
            title: "Implement aggressive staffing controls",
            detail: "Restrict leave, reassign personnel, and reduce nonurgent services.",
            result: "Short-term clinical coverage improves, but staff exhaustion and grievances rise.",
            stakeholder: "Nursing leadership challenges the fairness and safety of mandatory reassignments.",
            legal: "Employment rules, safety duties, collective agreements where applicable, and accommodation requirements need review.",
            reflection: "How do you protect staff without compromising patient care?",
            effects: { severity: -6, trust: -4, capacity: 12, legal: 12, pressure: 5, equity: -7, morale: -15 }
          },
          {
            title: "Use supported surge staffing",
            detail: "Recruit temporary support, offer accommodations, and prioritize care.",
            result: "The hospital stabilizes more slowly but preserves greater workforce cooperation.",
            stakeholder: "A finance officer warns that temporary staffing and support programs will be expensive.",
            legal: "Document transparent triage and staffing criteria while considering reasonable accommodations.",
            reflection: "How should limited resources be allocated fairly?",
            effects: { severity: -5, trust: 5, capacity: 8, legal: -4, pressure: 1, equity: 7, morale: 10 }
          },
          {
            title: "Maintain normal staffing policies",
            detail: "Rely on existing schedules and voluntary overtime.",
            result: "Immediate workplace conflict is limited, but service delays worsen.",
            stakeholder: "An emergency physician reports unsafe wait times and growing burnout.",
            legal: "Maintaining ordinary policies does not remove obligations to address foreseeable safety risks.",
            reflection: "At what point must normal operations be altered?",
            effects: { severity: 10, trust: -5, capacity: -17, legal: 7, pressure: 7, equity: -8, morale: -7 }
          }
        ]
      },
      {
        title: "Public Backlash",
        role: "Community Relations Director",
        story:
          "A social media post alleges that hospital policies favor affluent neighborhoods. A community leader disputes the county's case figures, and reporters demand a public response.",
        context:
          "Public communication must protect confidential information while addressing misinformation, uncertainty, and legitimate concerns about unequal access.",
        question: "How will your team respond publicly?",
        options: [
          {
            title: "Directly challenge public critics",
            detail: "Issue a strong statement defending the response and correcting disputed claims.",
            result: "The message is clear, but the conflict becomes more visible.",
            stakeholder: "A community organizer says officials are dismissing residents' lived experiences.",
            legal: "Accuracy and privacy are essential. Public disagreement should not become retaliation or unsupported disclosure.",
            reflection: "How can officials correct misinformation without silencing criticism?",
            effects: { severity: -2, trust: -12, capacity: 0, legal: 5, pressure: 13, equity: -5, morale: 1 }
          },
          {
            title: "Hold a transparent community briefing",
            detail: "Share verified information, acknowledge gaps, and invite participation.",
            result: "Trust improves, although the team faces difficult public questions.",
            stakeholder: "A local clinician requests translated updates and accessible vaccination services.",
            legal: "Communications should avoid identifiable patient information and unsupported claims.",
            reflection: "How will you show that community input changes policy?",
            effects: { severity: -4, trust: 13, capacity: -3, legal: -5, pressure: -7, equity: 10, morale: 4 }
          },
          {
            title: "Limit public comment",
            detail: "Release a brief written statement and avoid further media engagement.",
            result: "The organization avoids immediate confrontation, but rumors intensify.",
            stakeholder: "A reporter questions why leadership is withholding information.",
            legal: "Privacy duties do not generally justify withholding all aggregate public health information.",
            reflection: "What are the risks of remaining silent during uncertainty?",
            effects: { severity: 5, trust: -13, capacity: 0, legal: 4, pressure: 11, equity: -7, morale: -3 }
          }
        ]
      },
      {
        title: "Stabilization and Recovery",
        role: "Regional Emergency Coordinator",
        story:
          "The crisis enters its third week. Transmission appears to be slowing in some areas, but hospital staff are exhausted and residents are demanding a timeline for lifting emergency measures.",
        context:
          "The leadership team must distinguish temporary emergency actions from long-term policies and determine what evidence supports de-escalation.",
        question: "What recovery strategy will you adopt?",
        options: [
          {
            title: "Maintain broad emergency controls",
            detail: "Continue restrictions until case activity falls substantially.",
            result: "Risk remains controlled, but frustration and resource strain grow.",
            stakeholder: "Business and patient groups demand a clear justification for continuing restrictions.",
            legal: "Emergency measures require ongoing review for necessity, proportionality, and legal authority.",
            reflection: "What objective conditions would trigger repeal?",
            effects: { severity: -12, trust: -9, capacity: -8, legal: 10, pressure: 12, equity: -5, morale: -9 }
          },
          {
            title: "Use phased, evidence-based recovery",
            detail: "Set public thresholds, restore services gradually, and audit equity impacts.",
            result: "Recovery progresses with continued monitoring and transparent criteria.",
            stakeholder: "A patient representative requests a public review of delays and unequal treatment.",
            legal: "Documented criteria and review processes can strengthen accountability.",
            reflection: "How will the organization evaluate its emergency decisions?",
            effects: { severity: -7, trust: 11, capacity: 10, legal: -7, pressure: -7, equity: 10, morale: 9 }
          },
          {
            title: "End emergency measures immediately",
            detail: "Restore normal operations and leave future precautions voluntary.",
            result: "Some services recover quickly, but renewed transmission becomes a concern.",
            stakeholder: "Infection prevention staff warn that surveillance is insufficient.",
            legal: "The decision should consider available evidence and continuing duties to vulnerable populations.",
            reflection: "How would you respond if cases rise again?",
            effects: { severity: 13, trust: 2, capacity: 7, legal: 6, pressure: 4, equity: -7, morale: 5 }
          }
        ]
      }
    ];

    const initialState = {
      severity: 35,
      trust: 65,
      capacity: 70,
      legal: 20,
      pressure: 30,
      equity: 60,
      morale: 65
    };

    const gameState = {
      metrics: { ...initialState },
      currentRound: 0,
      selected: null,
      history: [],
      seconds: 45 * 60,
      timerId: null,
      paused: false,
      teamName: "Executive Leadership Team"
    };

    const $ = (id) => document.getElementById(id);

    function clamp(value) {
      return Math.max(0, Math.min(100, value));
    }

    function show(id) {
      $(id).classList.remove("hidden");
    }

    function hide(id) {
      $(id).classList.add("hidden");
    }

    function renderMetrics(targetId, metrics) {
      const target = $(targetId);
      target.replaceChildren();

      Object.keys(metricMeta).forEach((key) => {
        const card = document.createElement("div");
        card.className = "metric";

        const label = document.createElement("small");
        label.textContent = metricMeta[key];

        const value = document.createElement("strong");
        value.textContent = metrics[key] + "/100";

        const track = document.createElement("div");
        track.className = "track";

        const fill = document.createElement("div");
        fill.className = "fill";
        fill.style.width = metrics[key] + "%";

        track.appendChild(fill);
        card.append(label, value, track);
        target.appendChild(card);
      });
    }

    function renderDashboard() {
      renderMetrics("dashboard", gameState.metrics);
      renderMetrics("finalDashboard", gameState.metrics);
    }

    function updateTimerDisplay() {
      const minutes = Math.floor(gameState.seconds / 60);
      const seconds = gameState.seconds % 60;
      const timer = $("timer");
      timer.textContent = `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;
      timer.classList.toggle("late", gameState.seconds === 0);
    }

    function startTimer() {
      clearInterval(gameState.timerId);
      gameState.timerId = setInterval(() => {
        if (!gameState.paused && gameState.seconds > 0) {
          gameState.seconds -= 1;
          updateTimerDisplay();
        }

        if (gameState.seconds === 0) {
          clearInterval(gameState.timerId);
          $("timer").classList.add("late");
        }
      }, 1000);
    }

    function pauseTimer() {
      gameState.paused = !gameState.paused;
      $("pauseBtn").textContent = gameState.paused ? "Resume Timer" : "Pause Timer";
    }

    function buildContextNote() {
      const notes = [];
      const metrics = gameState.metrics;

      if (metrics.severity >= 60) {
        notes.push("Escalation: transmission is accelerating. The next decision carries greater clinical urgency.");
      }
      if (metrics.trust <= 40) {
        notes.push("Trust crisis: community groups now question official guidance and demand independent review.");
      }
      if (metrics.capacity <= 40) {
        notes.push("Capacity crisis: hospital leadership reports serious constraints on available services.");
      }
      if (metrics.legal >= 55) {
        notes.push("Legal challenge: counsel reports growing requests for documentation and review.");
      }
      if (metrics.equity <= 35) {
        notes.push("Equity warning: underserved neighborhoods report disproportionate barriers to care.");
      }

      return notes.join("\n\n");
    }

    function renderRound() {
      const round = rounds[gameState.currentRound];
      gameState.selected = null;

      $("roundLabel").textContent = `Round ${gameState.currentRound + 1} of ${rounds.length}`;
      $("phaseLabel").textContent =
        gameState.currentRound === 0
          ? "Briefing and initial response"
          : gameState.currentRound === rounds.length - 1
            ? "Stabilization and debrief"
            : "Escalating emergency response";

      $("progressFill").style.width = `${((gameState.currentRound + 1) / rounds.length) * 100}%`;
      $("roundRole").textContent = round.role;
      $("roundTitle").textContent = round.title;
      $("story").textContent = round.story;
      $("context").textContent = round.context;
      $("question").textContent = round.question;

      const optionContainer = $("options");
      optionContainer.replaceChildren();

      round.options.forEach((option, index) => {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "option";
        button.setAttribute("aria-pressed", "false");

        const title = document.createElement("strong");
        title.textContent = `${String.fromCharCode(65 + index)}. ${option.title}`;

        const detail = document.createElement("span");
        detail.textContent = option.detail;

        button.append(title, detail);
        button.addEventListener("click", () => selectOption(index));
        optionContainer.appendChild(button);
      });

      const customButton = document.createElement("button");
      customButton.type = "button";
      customButton.className = "option";
      customButton.textContent = "D. Propose an alternative or blended policy";
      customButton.setAttribute("aria-pressed", "false");
      customButton.addEventListener("click", () => selectOption(3));
      optionContainer.appendChild(customButton);

      $("customPolicy").value = "";
      $("reasoning").value = "";
      $("validation").textContent = "";
      hide("customBox");
      show("decisionPanel");
      hide("resultPanel");
      renderDashboard();

      const note = buildContextNote();
      if (note) {
        $("story").textContent += `\n\n${note}`;
      }
    }

    function selectOption(index) {
      gameState.selected = index;

      document.querySelectorAll(".option").forEach((button, i) => {
        const active = i === index;
        button.classList.toggle("selected", active);
        button.setAttribute("aria-pressed", String(active));
      });

      if (index === 3) {
        show("customBox");
      } else {
        hide("customBox");
      }
    }

    function applyEffects(effects) {
      Object.keys(gameState.metrics).forEach((key) => {
        gameState.metrics[key] = clamp(gameState.metrics[key] + (effects[key] || 0));
      });
    }

    function validateSubmission() {
      if (gameState.selected === null) {
        return "Please select a decision before continuing.";
      }

      const reasoning = $("reasoning").value.trim();
      if (reasoning.length < 20) {
        return "Please explain your reasoning in at least 20 characters.";
      }

      if (gameState.selected === 3) {
        const customText = $("customPolicy").value.trim();
        if (customText.length < 20) {
          return "Please describe your custom policy in more detail.";
        }
      }

      return "";
    }

    function computeWarningMessages(optionIndex) {
      const warnings = [];
      const metrics = gameState.metrics;

      if (metrics.severity >= 60) {
        warnings.push("High transmission magnifies the consequences of any delay or gaps in implementation.");
        if (optionIndex === 2) {
          gameState.metrics.severity = clamp(gameState.metrics.severity + 5);
        }
      }

      if (metrics.trust <= 40 && optionIndex === 0) {
        warnings.push("Low community trust increases resistance to restrictive policies.");
        gameState.metrics.trust = clamp(gameState.metrics.trust - 5);
      }

      if (metrics.capacity <= 40 && gameState.currentRound >= 2) {
        warnings.push("Existing hospital strain limits the effectiveness of this response.");
        gameState.metrics.capacity = clamp(gameState.metrics.capacity - 4);
      }

      return warnings;
    }

    function submitDecision() {
      $("validation").textContent = "";

      const validation = validateSubmission();
      if (validation) {
        $("validation").textContent = validation;
        return;
      }

      const round = rounds[gameState.currentRound];
      const selectedIndex = gameState.selected;

      let optionIndex = selectedIndex;
      let customText = "";

      if (selectedIndex === 3) {
        customText = $("customPolicy").value.trim();
        optionIndex = Number($("customStrategy").value);
      }

      const outcome = round.options[optionIndex];
      const warnings = computeWarningMessages(optionIndex);
      const before = { ...gameState.metrics };
      const reasoning = $("reasoning").value.trim();

      applyEffects(outcome.effects);

      const choiceTitle = selectedIndex === 3 ? `Custom policy: ${customText}` : outcome.title;

      gameState.history.push({
        round: gameState.currentRound + 1,
        title: round.title,
        choice: choiceTitle,
        strategy: outcome.title,
        reasoning,
        before,
        after: { ...gameState.metrics },
        consequence: outcome.result,
        stakeholder: outcome.stakeholder,
        legal: outcome.legal,
        warnings
      });

      $("resultText").textContent = outcome.result;
      $("stakeholder").textContent = outcome.stakeholder;
      $("legalText").textContent = outcome.legal + (warnings.length ? `\n\n${warnings.join(" ")}` : "");
      $("reflection").textContent = outcome.reflection;
      $("next").textContent = gameState.currentRound === rounds.length - 1 ? "View Final Debrief" : "Continue to Next Round";

      hide("decisionPanel");
      show("resultPanel");
      renderDashboard();
      $("resultPanel").scrollIntoView({ behavior: "smooth", block: "start" });
    }

    function nextRound() {
      gameState.currentRound += 1;

      if (gameState.currentRound >= rounds.length) {
        finishGame();
        return;
      }

      renderRound();
      $("decisionPanel").scrollIntoView({ behavior: "smooth", block: "start" });
    }

    function buildFinalNarrative() {
      const metrics = gameState.metrics;
      let narrative = "";

      if (metrics.severity >= 65) {
        narrative += "The outbreak remains difficult to control. ";
      } else if (metrics.severity <= 30) {
        narrative += "The response has substantially reduced the simulated outbreak severity. ";
      } else {
        narrative += "The outbreak shows partial stabilization. ";
      }

      if (metrics.trust <= 40) {
        narrative += "Public trust is fragile, complicating recovery. ";
      } else if (metrics.trust >= 70) {
        narrative += "Public trust is relatively strong, which supported recovery efforts. ";
      } else {
        narrative += "Public trust is mixed, requiring continued communication and accountability. ";
      }

      if (metrics.capacity <= 40) {
        narrative += "Hospital capacity remains a major risk to long-term operations. ";
      } else if (metrics.capacity >= 70) {
        narrative += "The system has regained enough operational capacity to function more steadily. ";
      } else {
        narrative += "Operational capacity is unstable but manageable. ";
      }

      if (metrics.legal >= 60) {
        narrative += "Legal exposure remains elevated and will likely require formal review of decisions. ";
      } else if (metrics.legal <= 30) {
        narrative += "Legal exposure is relatively contained, though future disputes remain possible. ";
      }

      return narrative.trim();
    }

    function finishGame() {
      clearInterval(gameState.timerId);
      hide("game");
      show("ending");
      $("finalNarrative").textContent = buildFinalNarrative();
      renderDashboard();
    }

    function downloadDecisionRecord() {
      const teamName = $("team").value.trim() || gameState.teamName;
      const reflection = $("finalReflection").value.trim() || "No final reflection provided.";
      const lines = [
        `Team: ${teamName}`,
        "",
        "Simulation Summary",
        "------------------",
        `Final narrative: ${$("finalNarrative").textContent}`,
        "",
        "Metric Summary",
        "--------------"
      ];

      Object.keys(metricMeta).forEach((key) => {
        lines.push(`${metricMeta[key]}: ${gameState.metrics[key]}/100`);
      });

      lines.push("", "Decision Record", "---------------");

      gameState.history.forEach((entry) => {
        lines.push(`Round ${entry.round}: ${entry.title}`);
        lines.push(`Choice: ${entry.choice}`);
        lines.push(`Reasoning: ${entry.reasoning}`);
        lines.push(`Consequence: ${entry.consequence}`);
        lines.push("");
      });

      lines.push("Final reflection");
      lines.push("----------------");
      lines.push(reflection);

      const blob = new Blob([lines.join("\n")], { type: "text/plain;charset=utf-8" });
      const url = URL.createObjectURL(blob);
      const link = document.createElement("a");
      link.href = url;
      link.download = `${(teamName || "public-health-response").replace(/\s+/g, "-").toLowerCase()}.txt`;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      URL.revokeObjectURL(url);
    }

    function resetGame() {
      clearInterval(gameState.timerId);
      gameState.metrics = { ...initialState };
      gameState.currentRound = 0;
      gameState.selected = null;
      gameState.history = [];
      gameState.seconds = 45 * 60;
      gameState.paused = false;
      gameState.teamName = $("team").value.trim() || "Executive Leadership Team";
      $("pauseBtn").textContent = "Pause Timer";
      updateTimerDisplay();
      renderDashboard();
      renderRound();
      startTimer();
      hide("ending");
      show("game");
      $("game").scrollIntoView({ behavior: "smooth", block: "start" });
    }

    function bindEvents() {
      $("start").addEventListener("click", resetGame);
      $("pauseBtn").addEventListener("click", () => {
        pauseTimer();
      });
      $("submitDecision").addEventListener("click", submitDecision);
      $("next").addEventListener("click", nextRound);
      $("download").addEventListener("click", downloadDecisionRecord);
      $("restart").addEventListener("click", () => {
        $("team").value = "";
        hide("ending");
        show("intro");
        hide("game");
        $("intro").scrollIntoView({ behavior: "smooth", block: "start" });
      });
    }

    document.addEventListener("DOMContentLoaded", () => {
      updateTimerDisplay();
      renderDashboard();
      bindEvents();
    });
  </script>
</body>
</html>
