<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>FlowTrack – Expense Tracker</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    /* ================== Base Styles ================== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      min-height: 100vh;
      background: radial-gradient(circle at top left, #2e8cff 0, #0b1020 40%, #050611 100%);
      color: #f5f7ff;
      display: flex;
      justify-content: center;
      align-items: stretch;
    }

    .app-wrapper {
      width: 100%;
      max-width: 1200px;
      margin: 20px;
      border-radius: 20px;
      background: linear-gradient(135deg, rgba(12, 19, 38, 0.98), rgba(18, 29, 62, 0.98));
      box-shadow:
        0 20px 40px rgba(0, 0, 0, 0.6),
        0 0 0 1px rgba(255, 255, 255, 0.02);
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }

    /* ================== Nav ================== */
    header {
      padding: 18px 28px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid rgba(255, 255, 255, 0.06);
      background: linear-gradient(120deg, rgba(19, 37, 80, 0.95), rgba(8, 13, 34, 0.95));
      backdrop-filter: blur(20px);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .brand-logo {
      width: 32px;
      height: 32px;
      border-radius: 12px;
      background: conic-gradient(from 140deg, #35ffe3, #46b2ff, #ff7bda, #ffd66b, #35ffe3);
      display: flex;
      align-items: center;
      justify-content: center;
      color: #050611;
      font-weight: 800;
      font-size: 18px;
      box-shadow: 0 8px 18px rgba(0, 0, 0, 0.5);
    }

    .brand-text {
      display: flex;
      flex-direction: column;
      line-height: 1.1;
    }

    .brand-text span:first-child {
      font-weight: 700;
      letter-spacing: 0.03em;
    }

    .brand-text span:last-child {
      font-size: 11px;
      opacity: 0.7;
      letter-spacing: 0.12em;
      text-transform: uppercase;
    }

    nav {
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 14px;
    }

    .nav-link {
      border: none;
      outline: none;
      padding: 8px 14px;
      border-radius: 999px;
      background: transparent;
      color: #d7ddff;
      cursor: pointer;
      transition: all 0.2s ease;
      font-size: 13px;
      letter-spacing: 0.04em;
      text-transform: uppercase;
    }

    .nav-link.active {
      background: radial-gradient(circle at top left, #46b2ff, #35ffe3);
      color: #050611;
      font-weight: 600;
      box-shadow: 0 6px 14px rgba(0, 0, 0, 0.4);
    }

    .nav-link:hover:not(.active) {
      background: rgba(255, 255, 255, 0.06);
    }

    .user-pill {
      padding: 6px 12px;
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.14);
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 12px;
      background: rgba(2, 6, 23, 0.8);
    }

    .user-status-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #ff6f91;
      box-shadow: 0 0 10px rgba(255, 111, 145, 0.7);
    }

    /* ================== Layout ================== */
    main {
      flex: 1;
      display: grid;
      grid-template-columns: minmax(0, 2.2fr) minmax(0, 2.8fr);
      gap: 0;
    }

    @media (max-width: 900px) {
      main {
        grid-template-columns: 1fr;
      }
    }

    .left-pane,
    .right-pane {
      padding: 24px 26px;
      overflow-y: auto;
      max-height: calc(100vh - 100px);
    }

    .left-pane {
      border-right: 1px solid rgba(255, 255, 255, 0.06);
      background: radial-gradient(circle at top left, rgba(70, 178, 255, 0.12), transparent 55%),
        radial-gradient(circle at bottom right, rgba(255, 123, 218, 0.16), transparent 45%);
    }

    .right-pane {
      background: radial-gradient(circle at top right, rgba(53, 255, 227, 0.14), transparent 60%);
    }

    h1,
    h2,
    h3 {
      font-weight: 700;
      letter-spacing: 0.03em;
    }

    h1 {
      font-size: 32px;
      margin-bottom: 6px;
    }

    h2 {
      font-size: 20px;
      margin-bottom: 10px;
    }

    h3 {
      font-size: 16px;
      margin-bottom: 8px;
    }

    p {
      font-size: 14px;
      opacity: 0.86;
    }

    /* ================== Hero / Home ================== */
    .badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.4);
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      margin-bottom: 12px;
      color: #e5e7eb;
    }

    .badge-dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: radial-gradient(circle, #35ffe3, #46b2ff);
      box-shadow: 0 0 12px rgba(53, 255, 227, 0.9);
    }

    .hero-subtitle {
      margin-bottom: 18px;
    }

    .hero-highlight {
      display: flex;
      gap: 12px;
      margin: 16px 0 26px;
      flex-wrap: wrap;
    }

    .chip {
      padding: 8px 12px;
      border-radius: 999px;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      border: 1px solid rgba(148, 163, 184, 0.5);
      background: rgba(15, 23, 42, 0.88);
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .chip-accent {
      background: radial-gradient(circle at top left, #46b2ff, #35ffe3);
      color: #050611;
      border: none;
    }

    .chip small {
      opacity: 0.75;
    }

    .cta-row {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 24px;
      flex-wrap: wrap;
    }

    .btn-primary {
      border: none;
      outline: none;
      padding: 10px 18px;
      border-radius: 999px;
      background: linear-gradient(135deg, #46b2ff, #35ffe3);
      color: #020617;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      box-shadow:
        0 12px 25px rgba(0, 0, 0, 0.6),
        0 0 0 1px rgba(15, 23, 42, 0.86);
      display: inline-flex;
      align-items: center;
      gap: 8px;
      letter-spacing: 0.04em;
      text-transform: uppercase;
    }

    .btn-primary span {
      font-size: 16px;
    }

    .btn-secondary {
      border-radius: 999px;
      padding: 9px 16px;
      border: 1px solid rgba(148, 163, 184, 0.55);
      background: rgba(15, 23, 42, 0.86);
      color: #e5e7eb;
      cursor: pointer;
      font-size: 13px;
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    .floating-note {
      font-size: 12px;
      display: flex;
      align-items: center;
      gap: 8px;
      opacity: 0.8;
    }

    .floating-note-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: #22c55e;
      box-shadow: 0 0 12px rgba(34, 197, 94, 0.9);
    }

    /* ================== Cards and Panels ================== */
    .panel {
      border-radius: 18px;
      padding: 16px 18px;
      background: radial-gradient(circle at top left, rgba(15, 23, 42, 0.9), rgba(2, 6, 23, 0.95));
      border: 1px solid rgba(148, 163, 184, 0.35);
      box-shadow: 0 10px 25px rgba(15, 23, 42, 0.9);
      margin-bottom: 16px;
    }

    .panel-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 10px;
    }

    .panel-header h3 {
      margin: 0;
    }

    .panel-header span {
      font-size: 11px;
      opacity: 0.75;
      text-transform: uppercase;
      letter-spacing: 0.12em;
    }

    /* ================== Login ================== */
    .section {
      display: none;
    }
    .section.active {
      display: block;
    }

    .login-form {
      display: flex;
      flex-direction: column;
      gap: 12px;
      margin-top: 8px;
    }

    .field {
      display: flex;
      flex-direction: column;
      gap: 4px;
      font-size: 13px;
    }

    label {
      opacity: 0.82;
    }

    input,
    select {
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.7);
      background: rgba(15, 23, 42, 0.96);
      color: #e5e7eb;
      padding: 8px 12px;
      font-size: 13px;
      outline: none;
      transition: border-color 0.18s ease, box-shadow 0.18s ease, background 0.18s ease;
    }

    input:focus,
    select:focus {
      border-color: #46b2ff;
      box-shadow: 0 0 0 1px rgba(70, 178, 255, 0.4);
      background: rgba(15, 23, 42, 0.98);
    }

    .error-text {
      margin-top: 4px;
      font-size: 11px;
      color: #fb7185;
      display: none;
    }

    .error-text.visible {
      display: block;
    }

    /* ================== Dashboard Top Stats ================== */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 12px;
      margin-top: 6px;
    }

    @media (max-width: 900px) {
      .stats-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    .stat-card {
      border-radius: 14px;
      padding: 10px 12px;
      background: radial-gradient(circle at top left, rgba(37, 99, 235, 0.18), rgba(15, 23, 42, 0.98));
      border: 1px solid rgba(148, 163, 184, 0.4);
      font-size: 12px;
    }

    .stat-label {
      opacity: 0.78;
      margin-bottom: 4px;
    }

    .stat-value {
      font-size: 20px;
      font-weight: 700;
    }

    .stat-meta {
      font-size: 11px;
      margin-top: 2px;
      opacity: 0.78;
    }

    .stat-positive {
      color: #4ade80;
    }

    .stat-negative {
      color: #fb7185;
    }

    /* ================== Expense Form ================== */
    .expense-form {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 10px;
      margin-top: 8px;
      align-items: flex-end;
    }

    @media (max-width: 900px) {
      .expense-form {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    .expense-form .field-full {
      grid-column: 1 / -1;
    }

    .btn-add {
      width: 100%;
      padding: 8px 12px;
      border-radius: 999px;
      border: none;
      outline: none;
      cursor: pointer;
      font-size: 13px;
      background: linear-gradient(135deg, #ff7bda, #ffd66b);
      color: #020617;
      font-weight: 600;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.6);
    }

    /* ================== Filters / Tabs ================== */
    .tabs {
      display: inline-flex;
      border-radius: 999px;
      padding: 3px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.5);
      margin: 8px 0 12px;
    }

    .tab-btn {
      border: none;
      outline: none;
      padding: 6px 12px;
      border-radius: 999px;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      background: transparent;
      color: #e5e7eb;
      cursor: pointer;
    }

    .tab-btn.active {
      background: radial-gradient(circle at top left, #46b2ff, #35ffe3);
      color: #020617;
      font-weight: 600;
    }

    .filter-row {
      display: flex;
      gap: 10px;
      align-items: center;
      flex-wrap: wrap;
      font-size: 12px;
      margin-bottom: 8px;
    }

    .filter-row span {
      opacity: 0.75;
    }

    .filter-row select,
    .filter-row input[type="date"] {
      font-size: 12px;
      padding: 6px 10px;
    }

    /* ================== Expense Table ================== */
    .table-wrapper {
      border-radius: 12px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      background: rgba(15, 23, 42, 0.95);
      overflow: hidden;
      max-height: 260px;
      display: flex;
      flex-direction: column;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
    }

    thead {
      background: rgba(15, 23, 42, 1);
      position: sticky;
      top: 0;
      z-index: 1;
    }

    th,
    td {
      padding: 8px 10px;
      text-align: left;
      border-bottom: 1px solid rgba(51, 65, 85, 0.8);
    }

    th {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      opacity: 0.7;
    }

    tbody tr:nth-child(even) {
      background: rgba(15, 23, 42, 0.96);
    }

    tbody tr:hover {
      background: rgba(30, 64, 175, 0.55);
    }

    .table-body {
      overflow-y: auto;
    }

    .amount-cell {
      font-weight: 600;
      color: #f97316;
    }

    /* ================== Graph ================== */
    .graph-wrapper {
      margin-top: 8px;
      border-radius: 14px;
      padding: 10px;
      background: radial-gradient(circle at top, rgba(15, 23, 42, 0.98), rgba(2, 6, 23, 0.98));
      border: 1px solid rgba(148, 163, 184, 0.45);
      box-shadow: 0 8px 20px rgba(15, 23, 42, 0.9);
    }

    .graph-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
      margin-bottom: 6px;
    }

    .graph-legend {
      display: flex;
      gap: 8px;
      align-items: center;
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.09em;
      opacity: 0.8;
    }

    .legend-color-block {
      width: 9px;
      height: 9px;
      border-radius: 999px;
      background: linear-gradient(135deg, #46b2ff, #35ffe3);
    }

    canvas {
      width: 100%;
      height: 160px;
    }

    /* ================== Summary ================== */
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
      margin-top: 8px;
      font-size: 12px;
    }

    @media (max-width: 900px) {
      .summary-grid {
        grid-template-columns: 1fr;
      }
    }

    .summary-card {
      border-radius: 14px;
      padding: 10px 12px;
      background: radial-gradient(circle at top left, rgba(236, 72, 153, 0.28), rgba(15, 23, 42, 0.96));
      border: 1px solid rgba(244, 114, 182, 0.7);
    }

    .summary-label {
      opacity: 0.78;
      margin-bottom: 4px;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
    }

    .summary-value {
      font-size: 18px;
      font-weight: 700;
    }

    .summary-detail {
      margin-top: 3px;
      font-size: 11px;
      opacity: 0.8;
    }

    .category-pills {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 6px;
    }

    .category-pill {
      padding: 4px 8px;
      border-radius: 999px;
      font-size: 11px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.5);
    }

    .footer-note {
      margin-top: 10px;
      font-size: 11px;
      opacity: 0.68;
    }
  </style>
</head>
<body>
  <div class="app-wrapper">
    <!-- ================== Header ================== -->
    <header>
      <div class="brand">
        <div class="brand-logo">ƒ</div>
        <div class="brand-text">
          <span>FlowTrack</span>
          <span>Where your money tells stories</span>
        </div>
      </div>
      <nav>
        <button class="nav-link active" data-target="home-section">Home</button>
        <button class="nav-link" data-target="login-section">Login</button>
        <button class="nav-link" data-target="dashboard-section">Dashboard</button>
        <div class="user-pill" id="userPill">
          <div class="user-status-dot"></div>
          <span id="userStatus">Guest Mode</span>
        </div>
      </nav>
    </header>

    <!-- ================== Main Content ================== -->
    <main>
      <!-- ========== LEFT PANE ========== -->
      <section class="left-pane">
        <!-- Home Section -->
        <div id="home-section" class="section active">
          <div class="badge">
            <div class="badge-dot"></div>
            FlowTrack · Personal expense story
          </div>
          <h1>Let your expenses speak clearly.</h1>
          <p class="hero-subtitle">
            FlowTrack turns scattered bills into a calm, visual story — by week, by month, by you.
          </p>

          <div class="hero-highlight">
            <div class="chip chip-accent">
              Weekly & Monthly view
              <small>See rhythms, not random numbers</small>
            </div>
            <div class="chip">
              <small>Designed for focus</small>
            </div>
            <div class="chip">
              <small>One-page. Zero clutter.</small>
            </div>
          </div>

          <div class="cta-row">
            <button class="btn-primary" id="startTrackingBtn">
              <span>●</span> Start tracking now
            </button>
            <button class="btn-secondary" id="goToLoginBtn">
              I already have a flow
            </button>
          </div>

          <div class="floating-note">
            <div class="floating-note-dot"></div>
            <span>No signup, no backend — your data lives only in this browser tab.</span>
          </div>

          <div class="panel" style="margin-top: 26px;">
            <div class="panel-header">
              <h3>What FlowTrack shows you</h3>
              <span>Preview</span>
            </div>
            <p>
              • How your week feels in numbers.<br />
              • Which category quietly drains you.<br />
              • A soft graph that rises and falls with your month.<br />
              • A summary that doesn’t judge — it just reflects.
            </p>
          </div>
        </div>

        <!-- Login Section -->
        <div id="login-section" class="section">
          <div class="panel">
            <div class="panel-header">
              <h2>Welcome back, storyteller.</h2>
              <span>Login</span>
            </div>
            <p>Give this session a name — a tiny ritual that says, “I’m paying attention now.”</p>

            <form class="login-form" id="loginForm">
              <div class="field">
                <label for="username">Session name</label>
                <input
                  type="text"
                  id="username"
                  placeholder="e.g. 'January Reset', 'College Budget', 'Calm Money'"
                  autocomplete="off"
                  required
                />
              </div>
              <div class="field">
                <label for="pin">Soft lock (4-digit PIN, optional)</label>
                <input
                  type="password"
                  id="pin"
                  placeholder="Just for you. Not enforced."
                  maxlength="4"
                  pattern="[0-9]*"
                />
                <div class="error-text" id="loginError">PIN must be exactly 4 digits.</div>
              </div>
              <button type="submit" class="btn-primary" style="margin-top: 6px;">
                <span>➤</span> Enter dashboard
              </button>
            </form>
          </div>

          <p style="font-size: 11px; opacity: 0.7; margin-top: 8px;">
            This is a front-end demo. There is no real authentication, just a gentle ritual of intention.
          </p>
        </div>

        <!-- Dashboard Section (Summary + Form) -->
        <div id="dashboard-section" class="section">
          <!-- Top stats -->
          <div class="panel">
            <div class="panel-header">
              <h2>This is your money’s rhythm.</h2>
              <span>Overview</span>
            </div>
            <p>Each entry is a line in your story. We simply arrange them so you can read it clearly.</p>

            <div class="stats-grid">
              <div class="stat-card">
                <div class="stat-label">This week</div>
                <div class="stat-value" id="statWeek">₹0</div>
                <div class="stat-meta stat-negative" id="statWeekMeta">0 entries</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">This month</div>
                <div class="stat-value" id="statMonth">₹0</div>
                <div class="stat-meta stat-negative" id="statMonthMeta">0 entries</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">All time</div>
                <div class="stat-value" id="statTotal">₹0</div>
                <div class="stat-meta" id="statTotalMeta">0 entries recorded</div>
              </div>
            </div>
          </div>

          <!-- Add expense -->
          <div class="panel">
            <div class="panel-header">
              <h3>Add a new expense</h3>
              <span>Capture the moment</span>
            </div>
            <form class="expense-form" id="expenseForm">
              <div class="field">
                <label for="expenseDate">Date</label>
                <input type="date" id="expenseDate" required />
              </div>
              <div class="field">
                <label for="expenseAmount">Amount (₹)</label>
                <input type="number" id="expenseAmount" min="0" step="0.01" placeholder="0.00" required />
              </div>
              <div class="field">
                <label for="expenseCategory">Category</label>
                <select id="expenseCategory">
                  <option value="Food">Food</option>
                  <option value="Transport">Transport</option>
                  <option value="Bills">Bills</option>
                  <option value="Shopping">Shopping</option>
                  <option value="Education">Education</option>
                  <option value="Other">Other</option>
                </select>
              </div>
              <div class="field field-full">
                <label for="expenseNote">Note (optional)</label>
                <input
                  type="text"
                  id="expenseNote"
                  placeholder="e.g. ‘Auto to college’, ‘Coffee with a friend’, ‘Online course’"
                />
              </div>
              <button class="btn-add" type="submit">Add to story</button>
            </form>
          </div>
        </div>
      </section>

      <!-- ========== RIGHT PANE ========== -->
      <section class="right-pane">
        <!-- Expenses + Graph -->
        <div class="panel">
          <div class="panel-header">
            <h3>Your expenses, week by week.</h3>
            <span>Timeline</span>
          </div>

          <!-- Tabs (Weekly / Monthly) -->
          <div class="tabs">
            <button class="tab-btn active" data-mode="weekly">Weekly</button>
            <button class="tab-btn" data-mode="monthly">Monthly</button>
          </div>

          <!-- Filters -->
          <div class="filter-row">
            <span>Focus on:</span>
            <select id="filterCategory">
              <option value="All">All categories</option>
              <option value="Food">Food</option>
              <option value="Transport">Transport</option>
              <option value="Bills">Bills</option>
              <option value="Shopping">Shopping</option>
              <option value="Education">Education</option>
              <option value="Other">Other</option>
            </select>

            <span>From:</span>
            <input type="date" id="filterFrom" />
            <span>To:</span>
            <input type="date" id="filterTo" />
          </div>

          <!-- Table -->
          <div class="table-wrapper">
            <div class="table-body">
              <table>
                <thead>
                  <tr>
                    <th>Date</th>
                    <th>Category</th>
                    <th>Note</th>
                    <th>Amount</th>
                  </tr>
                </thead>
                <tbody id="expenseTableBody">
                  <!-- Filled via JS -->
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- Graph -->
        <div class="graph-wrapper">
          <div class="graph-header">
            <span style="opacity: 0.78; font-size: 11px;">Visual rhythm</span>
            <div class="graph-legend">
              <div class="legend-color-block"></div>
              <span id="graphLegendText">Weekly totals</span>
            </div>
          </div>
          <canvas id="expenseChart"></canvas>
        </div>

        <!-- Summary -->
        <div class="panel" style="margin-top: 14px;">
          <div class="panel-header">
            <h3>Summary that just reflects.</h3>
            <span>Today’s snapshot</span>
          </div>

          <div class="summary-grid">
            <div class="summary-card">
              <div class="summary-label">Current view total</div>
              <div class="summary-value" id="summaryViewTotal">₹0</div>
              <div class="summary-detail" id="summaryViewMeta">No entries yet.</div>
            </div>

            <div class="summary-card">
              <div class="summary-label">Most frequent category</div>
              <div class="summary-value" id="summaryTopCategory">—</div>
              <div class="summary-detail" id="summaryTopCategoryMeta">We’ll highlight it once you add a few entries.</div>
            </div>
          </div>

          <div class="category-pills" id="summaryCategoryPills">
            <!-- Pills filled via JS -->
          </div>

          <p class="footer-note">
            You don’t have to fix everything at once. Start with noticing. FlowTrack is simply a mirror — gentle, clear,
            and honest.
          </p>
        </div>
      </section>
    </main>
  </div>

  <script>
    // ================== State ==================
    const state = {
      user: null,
      expenses: [],
      filter: {
        category: "All",
        from: null,
        to: null,
        mode: "weekly",
      },
    };

    // ================== Helpers ==================
    function formatCurrency(amount) {
      return "₹" + Number(amount).toFixed(2);
    }

    function parseDate(str) {
      return str ? new Date(str + "T00:00:00") : null;
    }

    function isSameWeek(dateA, dateB) {
      // Treat week start as Monday
      const d1 = new Date(dateA);
      const d2 = new Date(dateB);

      const day1 = (d1.getDay() + 6) % 7;
      const day2 = (d2.getDay() + 6) % 7;

      const monday1 = new Date(d1);
      monday1.setDate(d1.getDate() - day1);

      const monday2 = new Date(d2);
      monday2.setDate(d2.getDate() - day2);

      return (
        monday1.getFullYear() === monday2.getFullYear() &&
        monday1.getMonth() === monday2.getMonth() &&
        monday1.getDate() === monday2.getDate()
      );
    }

    function isSameMonth(dateA, dateB) {
      const d1 = new Date(dateA);
      const d2 = new Date(dateB);
      return d1.getFullYear() === d2.getFullYear() && d1.getMonth() === d2.getMonth();
    }

    function applyFilters(expenses) {
      const { category, from, to } = state.filter;
      return expenses.filter((e) => {
        const d = parseDate(e.date);
        if (!d) return false;

        if (category !== "All" && e.category !== category) return false;
        if (from && d < from) return false;
        if (to && d > to) return false;
        return true;
      });
    }

    // ================== DOM Elements ==================
    const navLinks = document.querySelectorAll(".nav-link");
    const sections = document.querySelectorAll(".section");
    const userPill = document.getElementById("userPill");
    const userStatus = document.getElementById("userStatus");

    const startTrackingBtn = document.getElementById("startTrackingBtn");
    const goToLoginBtn = document.getElementById("goToLoginBtn");

    const loginForm = document.getElementById("loginForm");
    const loginError = document.getElementById("loginError");

    const expenseForm = document.getElementById("expenseForm");
    const expenseTableBody = document.getElementById("expenseTableBody");

    const tabButtons = document.querySelectorAll(".tab-btn");
    const filterCategory = document.getElementById("filterCategory");
    const filterFrom = document.getElementById("filterFrom");
    const filterTo = document.getElementById("filterTo");

    const statWeek = document.getElementById("statWeek");
    const statWeekMeta = document.getElementById("statWeekMeta");
    const statMonth = document.getElementById("statMonth");
    const statMonthMeta = document.getElementById("statMonthMeta");
    const statTotal = document.getElementById("statTotal");
    const statTotalMeta = document.getElementById("statTotalMeta");

    const summaryViewTotal = document.getElementById("summaryViewTotal");
    const summaryViewMeta = document.getElementById("summaryViewMeta");
    const summaryTopCategory = document.getElementById("summaryTopCategory");
    const summaryTopCategoryMeta = document.getElementById("summaryTopCategoryMeta");
    const summaryCategoryPills = document.getElementById("summaryCategoryPills");

    const graphLegendText = document.getElementById("graphLegendText");

    const homeSection = document.getElementById("home-section");
    const loginSection = document.getElementById("login-section");
    const dashboardSection = document.getElementById("dashboard-section");

    const expenseDateInput = document.getElementById("expenseDate");

    // ================== Navigation ==================
    function showSection(sectionId) {
      sections.forEach((sec) => {
        sec.classList.toggle("active", sec.id === sectionId);
      });
      navLinks.forEach((link) => {
        link.classList.toggle("active", link.getAttribute("data-target") === sectionId);
      });
    }

    navLinks.forEach((link) => {
      link.addEventListener("click", () => {
        const target = link.getAttribute("data-target");
        showSection(target);
      });
    });

    startTrackingBtn.addEventListener("click", () => {
      showSection("dashboard-section");
    });

    goToLoginBtn.addEventListener("click", () => {
      showSection("login-section");
    });

    // ================== Login ==================
    loginForm.addEventListener("submit", (e) => {
      e.preventDefault();
      const username = document.getElementById("username").value.trim();
      const pin = document.getElementById("pin").value.trim();

      if (pin && pin.length !== 4) {
        loginError.classList.add("visible");
        return;
      } else {
        loginError.classList.remove("visible");
      }

      state.user = {
        name: username || "Quiet Session",
      };

      userStatus.textContent = state.user.name;
      showSection("dashboard-section");
    });

    // ================== Expense Adding ==================
    expenseForm.addEventListener("submit", (e) => {
      e.preventDefault();

      const date = document.getElementById("expenseDate").value;
      const amount = parseFloat(document.getElementById("expenseAmount").value);
      const category = document.getElementById("expenseCategory").value;
      const note = document.getElementById("expenseNote").value.trim();

      if (!date || isNaN(amount)) return;

      state.expenses.push({
        date,
        amount,
        category,
        note,
      });

      expenseForm.reset();
      setDefaultDateToToday();
      renderAll();
    });

    // ================== Filters ==================
    tabButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        tabButtons.forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        const mode = btn.getAttribute("data-mode");
        state.filter.mode = mode;
        graphLegendText.textContent = mode === "weekly" ? "Weekly totals" : "Monthly totals";
        renderAll();
      });
    });

    filterCategory.addEventListener("change", () => {
      state.filter.category = filterCategory.value;
      renderAll();
    });

    filterFrom.addEventListener("change", () => {
      state.filter.from = parseDate(filterFrom.value);
      renderAll();
    });

    filterTo.addEventListener("change", () => {
      state.filter.to = parseDate(filterTo.value);
      renderAll();
    });

    // ================== Rendering: Table ==================
    function renderTable() {
      const rows = applyFilters(state.expenses);
      expenseTableBody.innerHTML = "";

      if (rows.length === 0) {
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.colSpan = 4;
        td.textContent = "No expenses yet. Add your first one on the left.";
        td.style.opacity = "0.75";
        td.style.fontSize = "12px";
        tr.appendChild(td);
        expenseTableBody.appendChild(tr);
        return;
      }

      rows
        .slice()
        .sort((a, b) => new Date(b.date) - new Date(a.date))
        .forEach((exp) => {
          const tr = document.createElement("tr");

          const tdDate = document.createElement("td");
          tdDate.textContent = exp.date;

          const tdCategory = document.createElement("td");
          tdCategory.textContent = exp.category;

          const tdNote = document.createElement("td");
          tdNote.textContent = exp.note || "—";

          const tdAmount = document.createElement("td");
          tdAmount.textContent = formatCurrency(exp.amount);
          tdAmount.classList.add("amount-cell");

          tr.appendChild(tdDate);
          tr.appendChild(tdCategory);
          tr.appendChild(tdNote);
          tr.appendChild(tdAmount);
          expenseTableBody.appendChild(tr);
        });
    }

    // ================== Rendering: Stats ==================
    function renderStats() {
      const today = new Date();
      const all = state.expenses;

      let weekTotal = 0;
      let weekCount = 0;
      let monthTotal = 0;
      let monthCount = 0;
      let total = 0;

      all.forEach((e) => {
        const d = parseDate(e.date);
        total += e.amount;
        if (isSameWeek(d, today)) {
          weekTotal += e.amount;
          weekCount++;
        }
        if (isSameMonth(d, today)) {
          monthTotal += e.amount;
          monthCount++;
        }
      });

      statWeek.textContent = formatCurrency(weekTotal);
      statWeekMeta.textContent = weekCount + " entries this week";

      statMonth.textContent = formatCurrency(monthTotal);
      statMonthMeta.textContent = monthCount + " entries this month";

      statTotal.textContent = formatCurrency(total);
      statTotalMeta.textContent = all.length + " entries recorded";

      statWeekMeta.classList.toggle("stat-positive", weekTotal <= monthTotal / 4 && weekTotal > 0);
      statWeekMeta.classList.toggle("stat-negative", weekTotal > monthTotal / 4);
      statMonthMeta.classList.toggle("stat-negative", monthTotal > total / 2);
    }

    // ================== Rendering: Summary ==================
    function renderSummary() {
      const filtered = applyFilters(state.expenses);

      const total = filtered.reduce((sum, e) => sum + e.amount, 0);
      summaryViewTotal.textContent = formatCurrency(total);

      if (filtered.length === 0) {
        summaryViewMeta.textContent = "No entries in this view. Adjust filters or add a new expense.";
      } else {
        summaryViewMeta.textContent = filtered.length + " entries in this view.";
      }

      const categoryCounts = {};
      const categoryTotals = {};
      filtered.forEach((e) => {
        categoryCounts[e.category] = (categoryCounts[e.category] || 0) + 1;
        categoryTotals[e.category] = (categoryTotals[e.category] || 0) + e.amount;
      });

      let topCategory = null;
      let topCount = 0;
      Object.keys(categoryCounts).forEach((cat) => {
        if (categoryCounts[cat] > topCount) {
          topCount = categoryCounts[cat];
          topCategory = cat;
        }
      });

      if (!topCategory) {
        summaryTopCategory.textContent = "—";
        summaryTopCategoryMeta.textContent = "We’ll highlight it once you add a few entries.";
      } else {
        summaryTopCategory.textContent = topCategory;
        const catTotal = categoryTotals[topCategory];
        summaryTopCategoryMeta.textContent =
          topCount + " entries · " + formatCurrency(catTotal) + " in this view.";
      }

      summaryCategoryPills.innerHTML = "";
      Object.keys(categoryTotals)
        .sort((a, b) => categoryTotals[b] - categoryTotals[a])
        .forEach((cat) => {
          const pill = document.createElement("div");
          pill.className = "category-pill";
          pill.textContent = cat + " · " + formatCurrency(categoryTotals[cat]);
          summaryCategoryPills.appendChild(pill);
        });
    }

    // ================== Rendering: Graph ==================
    const canvas = document.getElementById("expenseChart");
    const ctx = canvas.getContext("2d");

    function resizeCanvas() {
      const rect = canvas.getBoundingClientRect();
      canvas.width = rect.width * window.devicePixelRatio;
      canvas.height = rect.height * window.devicePixelRatio;
      ctx.setTransform(window.devicePixelRatio, 0, 0, window.devicePixelRatio, 0, 0);
    }

    window.addEventListener("resize", () => {
      resizeCanvas();
      renderGraph();
    });

    function groupByWeek(expenses) {
      const map = new Map();
      expenses.forEach((e) => {
        const d = parseDate(e.date);
        if (!d) return;

        const day = (d.getDay() + 6) % 7;
        const monday = new Date(d);
        monday.setDate(d.getDate() - day);
        const key = monday.toISOString().slice(0, 10);

        map.set(key, (map.get(key) || 0) + e.amount);
      });

      const arr = Array.from(map.entries()).sort((a, b) => new Date(a[0]) - new Date(b[0]));
      return arr.map(([date, total]) => ({ label: date, total }));
    }

    function groupByMonth(expenses) {
      const map = new Map();
      expenses.forEach((e) => {
        const d = parseDate(e.date);
        if (!d) return;
        const key = d.getFullYear() + "-" + String(d.getMonth() + 1).padStart(2, "0");
        map.set(key, (map.get(key) || 0) + e.amount);
      });

      const arr = Array.from(map.entries()).sort((a, b) => new Date(a[0] + "-01") - new Date(b[0] + "-01"));
      return arr.map(([key, total]) => {
        const [year, month] = key.split("-");
        return { label: `${month}/${year.slice(2)}`, total };
      });
    }

    function renderGraph() {
      const filtered = applyFilters(state.expenses);
      let data;
      if (state.filter.mode === "weekly") {
        data = groupByWeek(filtered);
      } else {
        data = groupByMonth(filtered);
      }

      const width = canvas.width;
      const height = canvas.height;

      ctx.clearRect(0, 0, width, height);

      const padding = { top: 20, right: 20, bottom: 30, left: 40 };

      if (data.length === 0) {
        ctx.fillStyle = "rgba(148, 163, 184, 0.8)";
        ctx.font = "12px system-ui";
        ctx.fillText("Add some expenses to see your graph.", padding.left, height / 2);
        return;
      }

      const maxVal = Math.max(...data.map((d) => d.total)) || 1;
      const xStep = (width - padding.left - padding.right) / Math.max(data.length - 1, 1);
      const yScale = (height - padding.top - padding.bottom) / maxVal;

      // Grid lines
      ctx.strokeStyle = "rgba(148,163,184,0.3)";
      ctx.lineWidth = 1;
      ctx.setLineDash([4, 4]);
      const gridLines = 4;
      for (let i = 0; i <= gridLines; i++) {
        const y = padding.top + ((height - padding.top - padding.bottom) * i) / gridLines;
        ctx.beginPath();
        ctx.moveTo(padding.left, y);
        ctx.lineTo(width - padding.right, y);
        ctx.stroke();
      }
      ctx.setLineDash([]);

      // Line
      ctx.beginPath();
      data.forEach((point, index) => {
        const x = padding.left + xStep * index;
        const y = height - padding.bottom - point.total * yScale;
        if (index === 0) {
          ctx.moveTo(x, y);
        } else {
          ctx.lineTo(x, y);
        }
      });

      const gradient = ctx.createLinearGradient(padding.left, padding.top, width - padding.right, height);
      gradient.addColorStop(0, "#46b2ff");
      gradient.addColorStop(1, "#35ffe3");
      ctx.strokeStyle = gradient;
      ctx.lineWidth = 2;
      ctx.stroke();

      // Area fill
      ctx.lineTo(width - padding.right, height - padding.bottom);
      ctx.lineTo(padding.left, height - padding.bottom);
      ctx.closePath();
      const fillGradient = ctx.createLinearGradient(0, padding.top, 0, height - padding.bottom);
      fillGradient.addColorStop(0, "rgba(70,178,255,0.25)");
      fillGradient.addColorStop(1, "rgba(15,23,42,0.0)");
      ctx.fillStyle = fillGradient;
      ctx.fill();

      // Dots and labels
      ctx.fillStyle = "#35ffe3";
      data.forEach((point, index) => {
        const x = padding.left + xStep * index;
        const y = height - padding.bottom - point.total * yScale;
        ctx.beginPath();
        ctx.arc(x, y, 3, 0, Math.PI * 2);
        ctx.fill();
      });

      ctx.fillStyle = "rgba(148,163,184,0.9)";
      ctx.font = "10px system-ui";
      data.forEach((point, index) => {
        const x = padding.left + xStep * index;
        const y = height - padding.bottom - point.total * yScale;
        ctx.fillText(formatCurrency(point.total), x - 10, y - 6);
      });
    }

    // ================== Initial Setup ==================
    function setDefaultDateToToday() {
      const today = new Date();
      const yyyy = today.getFullYear();
      const mm = String(today.getMonth() + 1).padStart(2, "0");
      const dd = String(today.getDate()).padStart(2, "0");
      expenseDateInput.value = `${yyyy}-${mm}-${dd}`;
    }

    function renderAll() {
      renderTable();
      renderStats();
      renderSummary();
      renderGraph();
    }

    // Initialize
    resizeCanvas();
    setDefaultDateToToday();
    renderAll();
  </script>
</body>
</html>
