
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Public Health Crisis | Executive Simulation</title>
<style>
:root {
  --navy:#14263e;
  --blue:#245c85;
  --teal:#087e80;
  --light:#f3f6fa;
  --line:#dbe3ec;
  --ink:#243247;
  --red:#a72d36;
}
* {box-sizing:border-box}
body {
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:var(--light);
  color:var(--ink);
  line-height:1.55;
}
header {
  background:var(--navy);
  color:white;
  padding:25px max(20px,calc((100% - 1100px)/2));
}
header h1 {margin:0;font-size:1.8rem}
header p {margin:6px 0 0;color:#dce6f2}
main {max-width:1100px;margin:25px auto;padding:0 18px}
.panel {
  background:white;
  border:1px solid var(--line);
  border-radius:12px;
  padding:24px;
  margin-bottom:18px;
}
h2 {margin-top:0;color:var(--navy)}
h3 {color:var(--navy)}
button {
  font:inherit;
  cursor:pointer;
  border-radius:7px;
  border:1px solid var(--blue);
  background:var(--blue);
  color:white;
  padding:11px 17px;
  margin:5px 5px 5px 0;
}
button:hover {filter:brightness(.9)}
button:focus-visible,input:focus-visible,
textarea:focus-visible,select:focus-visible {
  outline:3px solid #e3a536;
  outline-offset:2px;
}
button.secondary {background:white;color:var(--blue)}
button:disabled {opacity:.5;cursor:not-allowed}
.hidden {display:none!important}
.grid {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:12px;
}
.metric {
  background:#f4f8fb;
  padding:14px;
  border-radius:9px;
  border:1px solid var(--line);
}
.metric strong {display:block;font-size:1.4rem}
.metric small {display:block;color:#526176}
.track {
  height:9px;background:#dce5ed;
  border-radius:10px;overflow:hidden;margin-top:9px;
}
.fill {height:100%;background:var(--teal);transition:width .4s}
.option {
  display:block;
  width:100%;
  text-align:left;
  margin:9px 0;
  background:white;
  color:var(--ink);
  border:2px solid var(--line);
  padding:16px;
}
.option:hover {background:#eef6fa}
.option.selected {
  border-color:var(--teal);
  background:#e9f6f4;
}
.option strong {display:block}
.option span {display:block;font-size:.94rem;margin-top:5px}
textarea,input,select {
  width:100%;
  padding:12px;
  border:1px solid #9cabbc;
  border-radius:7px;
  font:inherit;
  margin:7px 0 13px;
}
textarea {min-height:105px;resize:vertical}
label {display:block;font-weight:bold}
.callout {
  border-left:5px solid var(--teal);
  background:#eff8f7;
  padding:15px;
  margin:16px 0;
}
.warning {border-left-color:var(--red);background:#fff2f1}
.role {
  display:inline-block;
  background:#e9edf4;
  padding:4px 10px;
  border-radius:15px;
  font-size:.83rem;
  font-weight:bold;
  margin-bottom:8px;
}
.progress {
  height:9px;background:#dce5ed;
  border-radius:10px;overflow:hidden;
}
.progress div {height:100%;background:var(--teal)}
.topline {
  display:flex;
  justify-content:space-between;
  flex-wrap:wrap;
  gap:10px;
  align-items:center;
}
#timer {font-weight:bold;font-size:1.2rem}
#timer.late {color:var(--red)}
footer {text-align:center;padding:20px;color:#526176}
@media(max-width:600px){
  .panel{padding:17px}
  header h1{font-size:1.4rem}
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
  <span class="role">CONFIDENTIAL EXECUTIVE BRIEFING</span>
  <h2>Welcome to Redwood Valley</h2>
  <p>
    You are the executive leadership team responsible for
    coordinating a response to an escalating infectious
    disease emergency in fictional Redwood Valley.
  </p>
  <p>
    The region has approximately 240,000 residents,
    two hospitals, and a county public health department.
    A suspected measles outbreak has emerged following
    several large community gatherings.
  </p>
  <div class="callout">
    <strong>Your mission:</strong>
    Protect public health while navigating legal authority,
    patient rights, organizational constraints, equity,
    political pressure, and community trust.
  </div>
  <p>
    There is no single perfect solution. Your team must
    defend its choices and consider their consequences.
  </p>
  <label for="team">Executive team name</label>
  <input id="team" placeholder="Example: Team Redwood">
  <button id="start">Begin Simulation</button>
</section>

<div id="game" class="hidden">
  <section class="panel">
    <div class="topline">
      <strong id="roundLabel">Round 1 of 5</strong>
      <span id="timer" role="timer">45:00</span>
    </div>
    <div class="progress" aria-label="Simulation progress">
      <div id="progressFill" style="width:20%"></div>
    </div>
    <p id="phaseLabel"></p>
    <button class="secondary" id="pauseBtn">Pause Timer</button>
  </section>

  <section class="panel">
    <h2>Crisis Dashboard</h2>
    <p>
      These indicators are fictional teaching estimates,
      not epidemiological predictions or legal scores.
    </p>
    <div id="dashboard" class="grid"></div>
  </section>

  <section id="decisionPanel" class="panel">
    <span id="roundRole" class="role"></span>
    <h2 id="roundTitle"></h2>
    <p id="story"></p>
    <div id="context" class="callout"></div>
    <h3>Executive Decision</h3>
    <p id="question"></p>
    <div id="options"></div>

    <div id="customBox" class="hidden">
      <label for="customPolicy">Your proposed policy</label>
      <textarea id="customPolicy"
        placeholder="Describe your alternative or blended strategy.">
      </textarea>
      <label for="customStrategy">
        Which approach best describes your proposal?
      </label>
      <select id="customStrategy">
        <option value="0">Protective / precautionary</option>
        <option value="1">Balanced / targeted</option>
        <option value="2">Minimal intervention / voluntary</option>
      </select>
    </div>

    <label for="reasoning">
      Explain your team's legal and ethical reasoning
    </label>
    <textarea id="reasoning"
      placeholder="What authority applies? Who is affected? What tradeoffs are you accepting?">
    </textarea>
    <button id="submitDecision">Submit Executive Decision</button>
    <p id="validation" role="alert"></p>
  </section>

  <section id="resultPanel" class="panel hidden"
    aria-live="polite">
    <span class="role">CONSEQUENCE BRIEFING</span>
    <h2>Immediate Consequences</h2>
    <p id="resultText"></p>
    <h3>Stakeholder Response</h3>
    <div id="stakeholder" class="callout"></div>
    <h3>Legal and Ethical Considerations</h3>
    <p id="legalText"></p>
    <p><strong>Executive reflection:</strong>
      <span id="reflection"></span>
    </p>
    <button id="next">Continue to Next Round</button>
  </section>
</div>

<section id="ending" class="panel hidden">
  <span class="role">AFTER-ACTION REVIEW</span>
  <h2>Simulation Complete</h2>
  <p id="finalNarrative"></p>
  <div id="finalDashboard" class="grid"></div>

  <h3>Leadership Debrief</h3>
  <ol>
    <li>Which decision presented the greatest conflict
      between public safety and individual rights?</li>
    <li>Where did hospital authority end and public health
      authority begin?</li>
    <li>Which groups experienced disproportionate burdens?</li>
    <li>How did your communication choices affect trust?</li>
    <li>What would you change with better information?</li>
    <li>What safeguards would you require before
      implementing your most restrictive policy?</li>
  </ol>

  <label for="finalReflection">
    Final team reflection
  </label>
  <textarea id="finalReflection"
    placeholder="Summarize your most important leadership lessons.">
  </textarea>
  <button id="download">Download Decision Record</button>
  <button class="secondary" id="restart">Restart Simulation</button>
</section>
</main>

<footer>
  Fictional educational simulation.
  Not medical or legal advice.
</footer>

<script>
"use strict";

/*
  PUBLIC HEALTH CRISIS SIMULATION
  --------------------------------
  All content and branching rules are editable below.

  Indicator values range from 0 to 100.
  Higher trust, morale, equity, and capacity are better.
  Higher severity, legal exposure, and political
  pressure are worse.

  Custom policies are recorded verbatim, but their
  effects use the selected strategy category.
*/

const rounds = [
  {
    title:"First Alert",
    role:"County Health Director",
    story:
      "Redwood Valley confirms 12 measles cases. " +
      "Several patients visited schools, a crowded " +
      "community event, and a hospital emergency " +
      "department while potentially infectious. " +
      "Vaccination coverage varies substantially " +
      "across neighborhoods.",
    context:
      "The hospital can manage its facilities and " +
      "clinical operations. The county health " +
      "department must separately assess its " +
      "statutory authority for public health orders.",
    question:
      "How should your leadership team respond " +
      "during the first 24 hours?",
    options:[
      {
        title:"Launch a broad emergency response",
        detail:"Public warning, rapid tracing, expanded " +
          "testing and vaccination access.",
        result:"Response capacity expands quickly, but " +
          "some residents question the urgency.",
        stakeholder:"The mayor asks whether the public " +
          "announcement could create unnecessary panic.",
        legal:"Emergency messaging and resource " +
          "mobilization do not automatically authorize " +
          "compulsory restrictions.",
        reflection:"How would you explain the level " +
          "of uncertainty to the public?",
        effects:{severity:-9,trust:-3,capacity:-6,
          legal:3,pressure:9,equity:4,morale:-3}
      },
      {
        title:"Use a targeted, coordinated response",
        detail:"Notify affected groups, coordinate " +
          "clinical response, and expand voluntary services.",
        result:"Targeted action reduces disruption, " +
          "although some exposures remain unidentified.",
        stakeholder:"A school principal asks why " +
          "families outside the identified exposure " +
          "network have not been notified.",
        legal:"Targeting should rely on evidence, " +
          "consistent criteria, and equitable access.",
        reflection:"What evidence would justify " +
          "expanding the response?",
        effects:{severity:-5,trust:5,capacity:-3,
          legal:-3,pressure:2,equity:4,morale:2}
      },
      {
        title:"Begin with voluntary monitoring",
        detail:"Issue limited guidance and rely on " +
          "healthcare providers to report new cases.",
        result:"Initial disruption is limited, " +
          "but additional exposures go undetected.",
        stakeholder:"Emergency clinicians report " +
          "concern that the response is too slow.",
        legal:"Avoiding restrictions reduces some " +
          "liberty concerns but does not eliminate " +
          "institutional duties to respond.",
        reflection:"What is the ethical cost of delay?",
        effects:{severity:13,trust:1,capacity:-8,
          legal:5,pressure:6,equity:-6,morale:-7}
      }
    ]
  },
  {
    title:"Isolation Dispute",
    role:"Hospital Legal Counsel",
    story:
      "A patient with suspected measles refuses " +
      "recommended isolation and wishes to leave " +
      "the hospital. Several exposed individuals " +
      "have also declined voluntary guidance.",
    context:
      "Legal counsel cautions that clinical " +
      "recommendations, hospital infection-control " +
      "policies, and government isolation orders " +
      "involve different sources of authority.",
    question:
      "How will your team respond to the patient " +
      "and the broader exposure risk?",
    options:[
      {
        title:"Seek a formal isolation order",
        detail:"Request public health legal review " +
          "and pursue compulsory measures if authorized.",
        result:"Transmission risk is reduced, but " +
          "the intervention attracts scrutiny.",
        stakeholder:"A patient advocate demands " +
          "information about appeal rights, humane " +
          "conditions, and access to counsel.",
        legal:"Authority, procedural safeguards, " +
          "necessity, and least-restrictive alternatives " +
          "must be assessed under applicable law.",
        reflection:"What procedural protections " +
          "would make this intervention defensible?",
        effects:{severity:-11,trust:-9,capacity:-3,
          legal:12,pressure:10,equity:-7,morale:-2}
      },
      {
        title:"Negotiate supported voluntary isolation",
        detail:"Offer clear information, assistance, " +
          "and a defined reassessment process.",
        result:"Most individuals cooperate, " +
          "but some exposure risk persists.",
        stakeholder:"A social worker requests " +
          "transportation, food, and income support " +
          "for affected households.",
        legal:"Voluntary compliance may be more " +
          "sustainable when meaningful supports " +
          "address practical barriers.",
        reflection:"What happens if voluntary " +
          "cooperation fails?",
        effects:{severity:-5,trust:9,capacity:-5,
          legal:-5,pressure:-2,equity:9,morale:2}
      },
      {
        title:"Avoid compulsory measures",
        detail:"Provide advice and allow individuals " +
          "to determine whether to comply.",
        result:"Individual autonomy is preserved, " +
          "but additional contacts are exposed.",
        stakeholder:"A parent of an immunocompromised " +
          "child argues that the response ignores " +
          "vulnerable residents.",
        legal:"Respect for autonomy must be balanced " +
          "against foreseeable harms to others.",
        reflection:"When might nonintervention " +
          "become ethically unacceptable?",
        effects:{severity:15,trust:-5,capacity:-8,
          legal:7,pressure:9,equity:-10,morale:-5}
      }
    ]
  },
  {
    title:"Workforce Shortage",
    role:"Hospital Chief Operating Officer",
    story:
      "Hospital admissions are increasing. " +
      "Several staff members have been exposed, " +
      "and others are requesting leave. The " +
      "emergency department is approaching " +
      "its operational limits.",
    context:
      "The hospital must address patient safety, " +
      "employment obligations, infection control, " +
      "disability-related accommodations, and " +
      "equitable access to services.",
    question:
      "What workforce and service strategy " +
      "will your team adopt?",
    options:[
      {
        title:"Implement aggressive staffing controls",
        detail:"Restrict leave, reassign personnel, " +
          "and reduce nonurgent services.",
        result:"Short-term clinical coverage improves, " +
          "but staff exhaustion and grievances rise.",
        stakeholder:"Nursing leadership challenges " +
          "the fairness and safety of mandatory " +
          "reassignments.",
        legal:"Employment rules, safety duties, " +
          "collective agreements where applicable, " +
          "and accommodation requirements need review.",
        reflection:"How do you protect staff " +
          "without compromising patient care?",
        effects:{severity:-6,trust:-4,capacity:12,
          legal:12,pressure:5,equity:-7,morale:-15}
      },
      {
        title:"Use supported surge staffing",
        detail:"Recruit temporary support, " +
          "offer accommodations, and prioritize care.",
        result:"The hospital stabilizes more slowly " +
          "but preserves greater workforce cooperation.",
        stakeholder:"A finance officer warns that " +
          "temporary staffing and support programs " +
          "will be expensive.",
        legal:"Document transparent triage and " +
          "staffing criteria while considering " +
          "reasonable accommodations.",
        reflection:"How should limited resources " +
          "be allocated fairly?",
        effects:{severity:-5,trust:5,capacity:8,
          legal:-4,pressure:1,equity:7,morale:10}
      },
      {
        title:"Maintain normal staffing policies",
        detail:"Rely on existing schedules and " +
          "voluntary overtime.",
        result:"Immediate workplace conflict is " +
          "limited, but service delays worsen.",
        stakeholder:"An emergency physician reports " +
          "unsafe wait times and growing burnout.",
        legal:"Maintaining ordinary policies does " +
          "not remove obligations to address " +
          "foreseeable safety risks.",
        reflection:"At what point must normal " +
          "operations be altered?",
        effects:{severity:10,trust:-5,capacity:-17,
          legal:7,pressure:7,equity:-8,morale:-7}
      }
    ]
  },
  {
    title:"Public Backlash",
    role:"Community Relations Director",
    story:
      "A social media post alleges that hospital " +
      "policies favor affluent neighborhoods. " +
      "A community leader disputes the county's " +
      "case figures, and reporters demand a " +
      "public response.",
    context:
      "Public communication must protect " +
      "confidential information while addressing " +
      "misinformation, uncertainty, and legitimate " +
      "concerns about unequal access.",
    question:
      "How will your team respond publicly?",
    options:[
      {
        title:"Directly challenge public critics",
        detail:"Issue a strong statement defending " +
          "the response and correcting disputed claims.",
        result:"The message is clear, but " +
          "the conflict becomes more visible.",
        stakeholder:"A community organizer says " +
          "officials are dismissing residents' " +
          "lived experiences.",
        legal:"Accuracy and privacy are essential. " +
          "Public disagreement should not become " +
          "retaliation or unsupported disclosure.",
        reflection:"How can officials correct " +
          "misinformation without silencing criticism?",
        effects:{severity:-2,trust:-12,capacity:0,
          legal:5,pressure:13,equity:-5,morale:1}
      },
      {
        title:"Hold a transparent community briefing",
        detail:"Share verified information, " +
          "acknowledge gaps, and invite participation.",
        result:"Trust improves, although the " +
          "team faces difficult public questions.",
        stakeholder:"A local clinician requests " +
          "translated updates and accessible " +
          "vaccination services.",
        legal:"Communications should avoid " +
          "identifiable patient information " +
          "and unsupported claims.",
        reflection:"How will you show that " +
          "community input changes policy?",
        effects:{severity:-4,trust:13,capacity:-3,
          legal:-5,pressure:-7,equity:10,morale:4}
      },
      {
        title:"Limit public comment",
        detail:"Release a brief written statement " +
          "and avoid further media engagement.",
        result:"The organization avoids immediate " +
          "confrontation, but rumors intensify.",
        stakeholder:"A reporter questions why " +
          "leadership is withholding information.",
        legal:"Privacy duties do not generally " +
          "justify withholding all aggregate " +
          "public health information.",
        reflection:"What are the risks of " +
          "remaining silent during uncertainty?",
        effects:{severity:5,trust:-13,capacity:0,
          legal:4,pressure:11,equity:-7,morale:-3}
      }
    ]
  },
  {
    title:"Stabilization and Recovery",
    role:"Regional Emergency Coordinator",
    story:
      "The crisis enters its third week. " +
      "Transmission appears to be slowing in " +
      "some areas, but hospital staff are " +
      "exhausted and residents are demanding " +
      "a timeline for lifting emergency measures.",
    context:
      "The leadership team must distinguish " +
      "temporary emergency actions from " +
      "long-term policies and determine " +
      "what evidence supports de-escalation.",
    question:
      "What recovery strategy will you adopt?",
    options:[
      {
        title:"Maintain broad emergency controls",
        detail:"Continue restrictions until " +
          "case activity falls substantially.",
        result:"Risk remains controlled, " +
          "but frustration and resource strain grow.",
        stakeholder:"Business and patient groups " +
          "demand a clear justification for " +
          "continuing restrictions.",
        legal:"Emergency measures require " +
          "ongoing review for necessity, " +
          "proportionality, and legal authority.",
        reflection:"What objective conditions " +
          "would trigger repeal?",
        effects:{severity:-12,trust:-9,capacity:-8,
          legal:10,pressure:12,equity:-5,morale:-9}
      },
      {
        title:"Use phased, evidence-based recovery",
        detail:"Set public thresholds, restore " +
          "services gradually, and audit equity impacts.",
        result:"Recovery progresses with " +
          "continued monitoring and transparent criteria.",
        stakeholder:"A patient representative " +
          "requests a public review of delays " +
          "and unequal treatment.",
        legal:"Documented criteria and review " +
          "processes can strengthen accountability.",
        reflection:"How will the organization " +
          "evaluate its emergency decisions?",
        effects:{severity:-7,trust:11,capacity:10,
          legal:-7,pressure:-7,equity:10,morale:9}
      },
      {
        title:"End emergency measures immediately",
        detail:"Restore normal operations and " +
          "leave future precautions voluntary.",
        result:"Some services recover quickly, " +
          "but renewed transmission becomes a concern.",
        stakeholder:"Infection prevention staff " +
          "warn that surveillance is insufficient.",
        legal:"The decision should consider " +
          "available evidence and continuing " +
          "duties to vulnerable populations.",
        reflection:"How would you respond " +
          "if cases rise again?",
        effects:{severity:13,trust:2,capacity:7,
          legal:6,pressure:4,equity:-7,morale:5}
      }
    ]
  }
];

const initial = {
  severity:35,
  trust:65,
  capacity:70,
  legal:20,
  pressure:30,
  equity:60,
  morale:65
};

const labels = {
  severity:"Outbreak severity",
  trust:"Community trust",
  capacity:"Hospital capacity",
  legal:"Legal exposure",
  pressure:"Political pressure",
  equity:"Equity impact",
  morale:"Staff morale"
};

let state = {...initial};
let currentRound = 0;
let selected = null;
let history = [];
let seconds = 45*60;
let timerHandle = null;
let paused = false;
let teamName = "Executive Leadership Team";

const $ = id => document.getElementById(id);

function clamp(n) {
  return Math.max(0,Math.min(100,n));
}

function show(id) {
  $(id).classList.remove("hidden");
}
function hide(id) {
  $(id).classList.add("hidden");
}

function metricCards(target) {
  target.replaceChildren();

  Object.keys(labels).forEach(key => {
    const card = document.createElement("div");
    card.className = "metric";

    const label = document.createElement("small");
    label.textContent = labels[key];

    const value = document.createElement("strong");
    value.textContent = state[key] + "/100";

    const track = document.createElement("div");
    track.className = "track";

    const fill = document.createElement("div");
    fill.className = "fill";
    fill.style.width = state[key] + "%";

    track.append(fill);
    card.append(label,value,track);
    target.append(card);
  });
}

function updateDashboard() {
  metricCards($("dashboard"));
}

function updateTimer() {
  const m = Math.floor(seconds/60);
  const s = seconds%60;
  $("timer").textContent =
    String(m).padStart(2,"0") + ":" +
    String(s).padStart(2,"0");

  $("timer").classList.toggle("late",seconds===0);
}

function startTimer() {
  clearInterval(timerHandle);
  timerHandle = setInterval(() => {
    if (!paused && seconds>0) {
      seconds--;
      updateTimer();
    }
  },1000);
}

function renderRound() {
  const round = rounds[currentRound];
  selected = null;

  $("roundLabel").textContent =
    "Round " + (currentRound+1) + " of " + rounds.length;

  $("phaseLabel").textContent =
    currentRound===0 ? "Briefing and initial response" :
    currentRound===rounds.length-1 ?
      "Stabilization and debrief" :
      "Escalating emergency response";

  $("progressFill").style.width =
    ((currentRound+1)/rounds.length*100) + "%";

  $("roundRole").textContent = round.role;
  $("roundTitle").textContent = round.title;
  $("story").textContent = round.story;
  $("context").textContent = round.context;
  $("question").textContent = round.question;

  $("options").replaceChildren();

  round.options.forEach((option,index) => {
    const button = document.createElement("button");
    button.type = "button";
    button.className = "option";
    button.setAttribute("aria-pressed","false");

    const title = document.createElement("strong");
    title.textContent =
      String.fromCharCode(65+index) + ". " + option.title;

    const detail = document.createElement("span");
    detail.textContent = option.detail;

    button.append(title,detail);
    button.addEventListener("click",() => selectOption(index));
    $("options").append(button);
  });

  const custom = document.createElement("button");
  custom.type = "button";
  custom.className = "option";
  custom.textContent = "D. Propose an alternative or blended policy";
  custom.setAttribute("aria-pressed","false");
  custom.addEventListener("click",() => selectOption(3));
  $("options").append(custom);

  $("customPolicy").value = "";
  $("reasoning").value = "";
  $("validation").textContent = "";
  hide("customBox");
  show("decisionPanel");
  hide("resultPanel");
  updateDashboard();
}

function selectOption(index) {
  selected = index;

  document.querySelectorAll(".option").forEach((button,i) => {
    const active = i===index;
    button.classList.toggle("selected",active);
    button.setAttribute("aria-pressed",String(active));
  });

  if (index===3) show("customBox");
  else hide("customBox");
}

function applyEffects(effects) {
  for (const key of Object.keys(state)) {
    state[key] = clamp(state[key]+(effects[key]||0));
  }
}

/*
  Conditional branching:
  Prior decisions affect the context and consequences
  of subsequent rounds.
*/
function branchContext() {
  if (currentRound===0) return "";

  let notes = [];

  if (state.severity>=60) {
    notes.push(
      "Escalation: Transmission is accelerating. " +
      "The next decision carries greater clinical urgency."
    );
  }
  if (state.trust<=40) {
    notes.push(
      "Trust crisis: Community groups now question " +
      "official guidance and demand independent review."
    );
  }
  if (state.capacity<=40) {
    notes.push(
      "Capacity crisis: Hospital leadership reports " +
      "serious constraints on available services."
    );
  }
  if (state.legal>=55) {
    notes.push(
      "Legal challenge: Counsel reports growing " +
      "requests for documentation and review."
    );
  }
  if (state.equity<=35) {
    notes.push(
      "Equity warning: Underserved neighborhoods " +
      "report disproportionate barriers to care."
    );
  }

  return notes.join("\n\n");
}

function submitDecision() {
  $("validation").textContent = "";

  if (selected===null) {
    $("validation").textContent =
      "Please select a decision before continuing.";
    return;
  }

  const reasoning = $("reasoning").value.trim();
  if (reasoning.length<20) {
    $("validation").textContent =
      "Please explain your reasoning in at least 20 characters.";
    return;
  }

  let optionIndex = selected;
  let customText = "";

  if (selected===3) {
    customText = $("customPolicy").value.trim();

    if (customText.length<20) {
      $("validation").textContent =
        "Please describe your custom policy in more detail.";
      return;
    }
    optionIndex = Number($("customStrategy").value);
  }

  const round = rounds[currentRound];
  const outcome = round.options[optionIndex];
  const before = {...state};
  const warnings = [];

  if (state.severity>=60) {
    warnings.push(
      "High transmission magnifies the consequences " +
      "of any delay or gaps in implementation."
    );
    if (optionIndex===2) state.severity=clamp(state.severity+5);
  }

  if (state.trust<=40 && optionIndex===0) {
    warnings.push(
      "Low community trust increases resistance " +
      "to restrictive policies."
    );
    state.trust=clamp(state.trust-5);
  }

  if (state.capacity<=40 && currentRound>=2) {
    warnings.push(
      "Existing hospital strain limits " +
      "the effectiveness of this response."
    );
    state.capacity=clamp(state.capacity-4);
  }

  applyEffects(outcome.effects);

  const choiceTitle = selected===3 ?
    "Custom policy: " + customText :
    outcome.title;

  history.push({
    round:currentRound+1,
    title:round.title,
    choice:choiceTitle,
    strategy:outcome.title,
    reasoning,
    before,
    after:{...state},
    consequence:outcome.result,
    stakeholder:outcome.stakeholder,
    legal:outcome.legal,
    warnings
  });

  $("resultText").textContent = outcome.result;
  $("stakeholder").textContent = outcome.stakeholder;
  $("legalText").textContent =
    outcome.legal +
    (warnings.length ? "\n\n" + warnings.join(" ") : "");
  $("reflection").textContent = outcome.reflection;

  $("next").textContent =
    currentRound===rounds.length-1 ?
    "View Final Debrief" : "Continue to Next Round";

  hide("decisionPanel");
  show("resultPanel");
  updateDashboard();
  $("resultPanel").scrollIntoView({behavior:"smooth"});
}

function nextRound() {
  currentRound++;

  if (currentRound>=rounds.length) {
    finish();
    return;
  }

  renderRound();

  const extra = branchContext();
  if (extra) {
    $("story").textContent += "\n\n" + extra;
  }

  $("decisionPanel").scrollIntoView({behavior:"smooth"});
}

function finish() {
  clearInterval(timerHandle);
  hide("game");
  show("ending");

  let narrative = "";

  if (state.severity>=65) {
    narrative +=
      "The outbreak remains difficult to control. ";
  } else if (state.severity<=30) {
    narrative +=
      "The response has substantially reduced " +
      "the simulated outbreak severity. ";
  } else {
    narrative +=
      "The outbreak shows partial stabilization. ";
  }

  if (state.trust<=40) {
    narrative +=
      "Public trust is fragile, complicating recovery. ";
  } else if (state.trust>=70) {
    narrative +=
      "Community relationships provide a strong " +
      "foundation for recovery. ";
  }

  if (state.legal>=55) {
    narrative +=
      "Significant legal questions remain unresolved. ";
  }

  if (state.equity<=40) {
    narrative +=
      "The response also leaves substantial " +
      "equity concerns requiring corrective action. ";
  }

  narrative +=
    "These results are illustrative, not a grade. " +
    "Evaluate the justification and fairness " +
    "of each decision rather than treating " +
    "the dashboard as a definitive outcome.";

  $("finalNarrative").textContent = narrative;
  metricCards($("finalDashboard"));
  $("ending").scrollIntoView({behavior:"smooth"});
}

function downloadRecord() {
  const record = {
    simulation:"Public Health Crisis",
    team:teamName,
    completed:new Date().toISOString(),
    disclaimer:"Fictional educational simulation",
    decisions:history,
    finalIndicators:state,
    finalReflection:$("finalReflection").value.trim()
  };

  const blob = new Blob(
    [JSON.stringify(record,null,2)],
    {type:"application/json"}
  );

  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href=url;
  a.download="public-health-decision-record.json";
  document.body.append(a);
  a.click();
  a.remove();
  setTimeout(() => URL.revokeObjectURL(url),1000);
}

$("start").addEventListener("click",() => {
  teamName=$("team").value.trim() ||
    "Executive Leadership Team";
  hide("intro");
  show("game");
  renderRound();
  updateTimer();
  startTimer();
});

$("pauseBtn").addEventListener("click",() => {
  paused=!paused;
  $("pauseBtn").textContent =
    paused ? "Resume Timer" : "Pause Timer";
});

$("submitDecision").addEventListener("click",submitDecision);
$("next").addEventListener("click",nextRound);
$("download").addEventListener("click",downloadRecord);
$("restart").addEventListener("click",() => location.reload());

</script>
</body>
</html>
