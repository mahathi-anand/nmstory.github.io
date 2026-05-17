---
layout: post
title: RSVP <br>
description: <i>You are invited/Du bist eingeladen</i>
image: assets/images/collage.png
nav-menu: true
permalink: /rsvp/
show-tile: true
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RSVP</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

        :root {
            --gold:        #ffffff;
            --gold-light:  #161a34;
            --gold-pale:   #242943;
            --bg:          #242943;
            --card:        #242943;
            --text:        #ffffff;
            --muted:       #666666;
            --border:      #161a34;
            --red:         #C0392B;
            --green:       #27AE60;
        }

        
        
        /* ── Tabs ─────────────────────────────────────────────────── */
        .tabs {
            display: flex;
            border-radius: 12px;
            overflow: hidden;
            border: 2px solid var(--border);
            margin-bottom: 32px;
            background: white;
        }
        .tab-btn {
            flex: 1;
            padding: 14px 10px;
            border: none;
            background: transparent;
            cursor: pointer;
            font-size: .95em;
            font-family: inherit;
            color: var(--muted);
            transition: background .18s, color .18s;
            font-weight: 600;
        }
        .tab-btn.active {
            background: var(--gold);
            color: #fff;
        }

        /* ── Card ─────────────────────────────────────────────────── */
        .form-card {
            background: var(--card);
            border-radius: 18px;
            padding: clamp(24px, 5vw, 44px);
            box-shadow: 0 6px 32px rgba(0,0,0,.07);
            border: 1px solid var(--border);
        }

        /* ── Form sections ────────────────────────────────────────── */
        .section + .section { margin-top: 32px; }
        .section-title {
            font-size: .78em;
            text-transform: uppercase;
            letter-spacing: .12em;
            color: var(--gold);
            margin-bottom: 18px;
            padding-bottom: 8px;
            border-bottom: 1px solid var(--border);
            font-family: system-ui, sans-serif;
            font-weight: 700;
        }

        .field { margin-bottom: 16px; }
        label {
            display: block;
            font-size: .88em;
            font-weight: 700;
            color: var(--text);
            margin-bottom: 6px;
            font-family: system-ui, sans-serif;
        }
        label .opt {
            font-weight: 400;
            color: var(--muted);
        }
        .req { color: var(--red); }

        input[type="text"],
        input[type="email"],
        input[type="tel"],
        textarea {
            width: 100%;
            padding: 10px 13px;
            border: 1.5px solid var(--border);
            border-radius: 8px;
            font-size: .97em;
            font-family: inherit;
            color: var(--text);
            background: var(--bg);
            outline: none;
            transition: border-color .18s, background .18s;
        }
        input:focus, textarea:focus {
            border-color: var(--gold);
            background: #000000;
        }
        input.invalid, textarea.invalid {
            border-color: var(--red);
        }
        textarea { resize: vertical; min-height: 84px; }

        .field-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
        }
        @media (max-width: 520px) { .field-row { grid-template-columns: 1fr; } }

        .field-error {
            color: var(--red);
            font-size: .8em;
            margin-top: 4px;
            display: none;
            font-family: system-ui, sans-serif;
        }

        /* ── Dynamic guest rows ───────────────────────────────────── */
        .guest-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 10px; }
        .guest-row  { display: flex; gap: 8px; align-items: center; }
        .guest-row input { flex: 1; }

        .btn-icon {
            width: 34px; height: 36px;
            background: none;
            border: 1.5px solid #E0C0C0;
            color: var(--red);
            border-radius: 7px;
            cursor: pointer;
            font-size: 1.1em;
            display: flex; align-items: center; justify-content: center;
            flex-shrink: 0;
            transition: background .15s;
        }
        .btn-icon:hover { background: #FDECEA; }

        .btn-add {
            background: none;
            border: 1.5px dashed var(--gold-light);
            color: var(--gold);
            padding: 8px 16px;
            border-radius: 8px;
            cursor: pointer;
            font-size: .88em;
            font-family: system-ui, sans-serif;
            transition: background .15s;
        }
        .btn-add:hover { background: var(--gold-pale); }

        /* ── Consent box ──────────────────────────────────────────── */
        .consent-label {
            display: flex;
            gap: 12px;
            align-items: flex-start;
            padding: 16px;
            background: var(--gold-pale);
            border-radius: 10px;
            border: 1px solid var(--border);
            cursor: pointer;
        }
        .consent-label input[type="checkbox"] {
            width: 20px; height: 20px;
            margin-top: 2px;
            flex-shrink: 0;
            accent-color: var(--gold);
            cursor: pointer;
        }
        .consent-label span {
            font-size: .88em;
            line-height: 1.55;
            color: var(--text);
            font-family: system-ui, sans-serif;
        }

        /* ── Submit ───────────────────────────────────────────────── */
        .btn-submit {
            width: 100%;
            padding: 14px;
            background: var(--gold-light);
            color: #fff;
            border: none;
            border-radius: 10px;
            font-size: 1.05em;
            font-family: inherit;
            cursor: pointer;
            margin-top: 28px;
            transition: background .2s, transform .1s;
            letter-spacing: .03em;
        }
        .btn-submit:hover   { background: #303030; }
        .btn-submit:active  { transform: scale(.99); }
        .btn-submit:disabled { opacity: .7; cursor: not-allowed; }

        .spinner {
            display: inline-block;
            width: 16px; height: 16px;
            border: 2px solid rgba(255,255,255,.4);
            border-top-color: #fff;
            border-radius: 50%;
            animation: spin .7s linear infinite;
            vertical-align: middle;
            margin-right: 6px;
        }
        @keyframes spin { to { transform: rotate(360deg); } }

        /* ── Success ──────────────────────────────────────────────── */
        .success-msg {
            display: none;
            text-align: center;
            padding: 56px 32px;
            background: var(--card);
            border-radius: 18px;
            box-shadow: 0 6px 32px rgba(0,0,0,.07);
            border: 1px solid var(--border);
        }
        .success-msg.visible { display: block; }
        .success-icon { font-size: 3em; margin-bottom: 18px; }
        .success-msg h2 {
            font-size: 1.9em;
            font-weight: normal;
            color: var(--gold);
            margin-bottom: 12px;
        }
        .success-msg p {
            color: var(--muted);
            line-height: 1.7;
            font-family: system-ui, sans-serif;
            font-size: .95em;
        }

        /* ── Admin trigger ────────────────────────────────────────── */
        .admin-trigger {
            display: block;
            margin: 56px auto 0;
            background: none;
            border: none;
            color: #DDD;
            font-size: .72em;
            cursor: pointer;
            font-family: system-ui, sans-serif;
            letter-spacing: .06em;
        }
        .admin-trigger:hover { color: #AAA; }

        /* ── Admin panel ──────────────────────────────────────────── */
        #admin-panel { display: none; margin-top: 8px; }
        #admin-panel.visible { display: block; }

        .admin-login {
            max-width: 340px;
            margin: 0 auto;
            text-align: center;
            padding: 36px 24px;
            background: var(--card);
            border-radius: 16px;
            border: 1px solid var(--border);
        }
        .admin-login h3 {
            color: var(--gold);
            font-weight: normal;
            font-size: 1.3em;
            margin-bottom: 20px;
        }
        .admin-login input { margin-bottom: 12px; }

        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 20px;
        }
        .admin-header h2 {
            font-weight: normal;
            color: var(--gold);
            font-size: 1.3em;
        }
        .btn-export {
            padding: 8px 16px;
            background: var(--green);
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: .88em;
            font-family: system-ui, sans-serif;
        }
        .btn-danger {
            padding: 8px 16px;
            background: var(--red);
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: .88em;
            font-family: system-ui, sans-serif;
            margin-left: 8px;
        }

        .admin-note {
            background: #EFF8FF;
            border: 1px solid #BCD9F0;
            border-radius: 8px;
            padding: 10px 14px;
            font-size: .82em;
            color: #1A5276;
            margin-bottom: 18px;
            font-family: system-ui, sans-serif;
            line-height: 1.5;
        }

        .table-wrap { overflow-x: auto; border-radius: 12px; }
        .rsvp-table {
            width: 100%;
            border-collapse: collapse;
            font-size: .83em;
            background: white;
            font-family: system-ui, sans-serif;
        }
        .rsvp-table th {
            background: var(--gold);
            color: #fff;
            padding: 10px 13px;
            text-align: left;
            font-weight: 600;
            white-space: nowrap;
        }
        .rsvp-table td {
            padding: 10px 13px;
            border-bottom: 1px solid var(--border);
            vertical-align: top;
        }
        .rsvp-table tr:last-child td { border-bottom: none; }
        .rsvp-table tr:nth-child(even) td { background: var(--bg); }
        .rsvp-table .empty-row td {
            text-align: center;
            color: #999;
            padding: 28px;
        }

        .badge {
            display: inline-block;
            padding: 2px 9px;
            border-radius: 20px;
            font-size: .78em;
            font-weight: 700;
        }
        .badge-intl  { background: #EBF5FB; color: #1A5276; }
        .badge-local { background: #EAFAF0; color: #1A6A3A; }
    </style>
</head>
<body>

<!-- ═══════════════════════════════ HERO ═══════════════════════════════════ -->
<div class="hero">
    <p class="hero-sub"></p>
    <h1>Please RSVP</h1>
    <p>Kindly confirm your attendance and let us know a few details so we can make the day perfect for everyone.</p>
    <p>Wedding Venue: <a href="https://browntownresort.com/" target="_blank">Brown Town Resort, Spa &amp; Convention</a><br>
     Dates: 10th and 11th December, 2026</p>
    <p>Note that accommodations for the wedding dates are included. <br>
    Check-in: 10th December, 2:00pm. Check-out: 12th December, 11:00am </p>
    <p>Other details will follow soon. Stay tuned for more updates in the website. </p> 

</div>

<!-- ═══════════════════════════════ MAIN ═══════════════════════════════════ -->
<div class="container">

    <!-- RSVP Form -->
    <div class="form-card" id="form-card">
        <form id="rsvp-form" novalidate autocomplete="on">
            <input type="hidden" name="_guest_type" id="f_guest_type" value="International">

            <!-- ── Your Details ─────────────────────────────────── -->
            <div class="section">
                <p class="section-title">Your Details</p>

                <div class="field">
                    <label for="f_name">Full Name <span class="req">*</span></label>
                    <input type="text" id="f_name" name="name"
                           placeholder="First and last name"
                           autocomplete="name" required>
                    <div class="field-error" id="err_name">Please enter your full name.</div>
                </div>

                <div class="field-row">
                    <div class="field" style="margin-bottom:0">
                        <label for="f_email">Email Address <span class="req">*</span></label>
                        <input type="email" id="f_email" name="email"
                               placeholder="you@example.com"
                               autocomplete="email" required>
                        <div class="field-error" id="err_email">Please enter a valid email address.</div>
                    </div>
                    <div class="field" style="margin-bottom:0">
                        <label for="f_mobile">Mobile Number <span class="req">*</span></label>
                        <input type="tel" id="f_mobile" name="mobile"
                               placeholder="+1 234 567 8900"
                               autocomplete="tel" required>
                        <div class="field-error" id="err_mobile">Please enter your mobile number.</div>
                    </div>
                </div>
            </div>

            <!-- ── Additional Guests ────────────────────────────── -->
            <div class="section">
                <p class="section-title">Additional Guests <span style="font-weight:400; font-size:.9em; text-transform:none; letter-spacing:0">(optional)</span></p>
                <div class="guest-list" id="adult-list" aria-label="Additional adult guests"></div>
                <button type="button" class="btn-add" onclick="addGuest('adult')">+ Add adult guest</button>
            </div>

            <!-- ── Children ─────────────────────────────────────── -->
            <div class="section">
                <p class="section-title">Children <span style="font-weight:400; font-size:.9em; text-transform:none; letter-spacing:0">(optional)</span></p>
                <div class="guest-list" id="kids-list" aria-label="Children"></div>
                <button type="button" class="btn-add" onclick="addGuest('kid')">+ Add child's name</button>
            </div>

            <!-- ── Dietary ──────────────────────────────────────── -->
            <div class="section">
                <p class="section-title">Dietary Restrictions &amp; Allergies</p>
                <div class="field" style="margin-bottom:0">
                    <label for="f_dietary">
                        Please list any dietary requirements or allergies
                        <span class="opt">(leave blank if none)</span>
                    </label>
                    <textarea id="f_dietary" name="dietary"
                              placeholder="e.g. vegetarian, gluten-free, nut allergy, lactose intolerant…"></textarea>
                </div>
            </div>

            <!-- ── WhatsApp ─────────────────────────────────────── -->
            <div class="section">
                <p class="section-title">WhatsApp Planning Group</p>
                <label class="consent-label" for="f_whatsapp">
                    <input type="checkbox" id="f_whatsapp" name="whatsapp_consent" value="yes">
                    <span>
                        I agree to be added to the WhatsApp group for event planning and information updates.
                        The mobile number I provided above will be used for this purpose.
                    </span>
                </label>
            </div>

            <button type="submit" class="btn-submit" id="submit-btn">Confirm my RSVP</button>
        </form>
    </div>

    <!-- Success screen -->
    <div class="success-msg" id="success-msg" role="alert">
        <div class="success-icon">🎉</div>
        <h2>Thank you!</h2>
        <p>
            Your RSVP has been received. We look forward to celebrating with you!<br><br>
            If you opted in to the WhatsApp group, you will receive an invitation to join soon.
        </p>
    </div>

    <!-- Admin trigger (visually hidden until hovered) -->
    <button class="admin-trigger" onclick="toggleAdmin()" aria-label="Admin access">admin</button>

    <!-- ═══════════════════ ADMIN PANEL ══════════════════════════════════ -->
    <div id="admin-panel" role="region" aria-label="Admin panel">

        <!-- Login form -->
        <div class="admin-login" id="admin-login">
            <h3>Admin Access</h3>
            <input type="password" id="admin-pass" placeholder="Password"
                   onkeydown="if(event.key==='Enter') checkAdminPass()">
            <button onclick="checkAdminPass()" class="btn-submit" style="margin-top:4px;">Login</button>
            <div id="admin-err" style="color:var(--red); font-size:.82em; margin-top:8px; display:none; font-family:system-ui,sans-serif;">
                Incorrect password.
            </div>
        </div>

        <!-- Content (shown after login) -->
        <div id="admin-content" style="display:none;">
            <div class="admin-note">
                ℹ️ This table shows submissions stored on <strong>this device</strong>.
                All submissions from guests on their own devices are saved in your
                <strong>Google Sheet</strong> (RSVPs tab) — export anytime via
                <em>File → Download → CSV</em>.
            </div>

            <div class="admin-header">
                <h2>RSVP Submissions &nbsp;<span id="rsvp-count" style="color:var(--muted); font-size:.85em;">0 entries</span></h2>
                <div>
                    <button class="btn-export" onclick="exportCSV()">⬇ Export CSV</button>
                    <button class="btn-danger" onclick="clearData()">🗑 Clear All</button>
                </div>
            </div>

            <div class="table-wrap">
                <table class="rsvp-table" id="rsvp-table">
                    <thead>
                        <tr>
                            <th>#</th>
                            <th>Type</th>
                            <th>Name</th>
                            <th>Email</th>
                            <th>Mobile</th>
                            <th>Additional Guests</th>
                            <th>Children</th>
                            <th>Dietary / Allergies</th>
                            <th>WhatsApp</th>
                            <th>Submitted</th>
                        </tr>
                    </thead>
                    <tbody id="rsvp-tbody"></tbody>
                </table>
            </div>
        </div>

    </div><!-- /admin-panel -->

</div><!-- /container -->

<!-- ═══════════════════════════════ SCRIPT ═════════════════════════════════ -->
<script>
// ─── CONFIGURATION — edit these two values ──────────────────────────────────
const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbx9nC_7zHAAR6zwvOdidxJKpeTEiybVSnEyTAGRdod0SxXx41BFIzYYXExNt_KTB1HKRg/exec'; // paste your Apps Script Web App URL
const ADMIN_PASSWORD    = 'df1263s5dsf3';               // change to something secure
// ────────────────────────────────────────────────────────────────────────────

const LS_KEY = 'rsvp_submissions';

let adminUnlocked = false;

// ── Tab switching ─────────────────────────────────────────────────────────
function switchTab(tab) {
    const isIntl = tab === 'international';
    document.getElementById('f_guest_type').value = isIntl ? 'International' : 'Local';
    document.getElementById('tab-intl').classList.toggle('active', isIntl);
    document.getElementById('tab-local').classList.toggle('active', !isIntl);
}

// ── Dynamic guest rows ────────────────────────────────────────────────────
function addGuest(type) {
    const listId     = type === 'adult' ? 'adult-list' : 'kids-list';
    const placeholder = type === 'adult' ? 'Guest full name' : "Child's name";
    const list = document.getElementById(listId);

    const row = document.createElement('div');
    row.className = 'guest-row';
    row.innerHTML =
        `<input type="text" class="${type}-name" placeholder="${placeholder}" aria-label="${placeholder}">` +
        `<button type="button" class="btn-icon" aria-label="Remove" onclick="this.parentElement.remove()">×</button>`;
    list.appendChild(row);
    row.querySelector('input').focus();
}

function collectNames(cssClass) {
    return [...document.querySelectorAll(`.${cssClass}`)]
        .map(i => i.value.trim()).filter(Boolean).join(', ');
}

// ── Validation ────────────────────────────────────────────────────────────
function validateForm() {
    const rules = [
        {
            id: 'f_name',  errId: 'err_name',
            ok: v => v.trim().length >= 2
        },
        {
            id: 'f_email', errId: 'err_email',
            ok: v => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v.trim())
        },
        {
            id: 'f_mobile', errId: 'err_mobile',
            ok: v => v.trim().replace(/\D/g, '').length >= 6
        },
    ];

    let valid = true;
    rules.forEach(({ id, errId, ok }) => {
        const el  = document.getElementById(id);
        const err = document.getElementById(errId);
        const pass = ok(el.value);
        el.classList.toggle('invalid', !pass);
        err.style.display = pass ? 'none' : 'block';
        if (!pass) valid = false;
    });
    return valid;
}

// Clear validation state on input
['f_name', 'f_email', 'f_mobile'].forEach(id => {
    document.getElementById(id).addEventListener('input', () => {
        const el = document.getElementById(id);
        el.classList.remove('invalid');
        document.getElementById('err_' + id.replace('f_', '')).style.display = 'none';
    });
});

// ── Form submission ───────────────────────────────────────────────────────
document.getElementById('rsvp-form').addEventListener('submit', async (e) => {
    e.preventDefault();
    if (!validateForm()) return;

    const btn = document.getElementById('submit-btn');
    btn.innerHTML = '<span class="spinner"></span>Sending…';
    btn.disabled = true;

    const entry = {
        guest_type:        document.getElementById('f_guest_type').value,
        name:              document.getElementById('f_name').value.trim(),
        email:             document.getElementById('f_email').value.trim(),
        mobile:            document.getElementById('f_mobile').value.trim(),
        additional_guests: collectNames('adult-name'),
        children:          collectNames('kid-name'),
        dietary:           document.getElementById('f_dietary').value.trim(),
        whatsapp_consent:  document.getElementById('f_whatsapp').checked ? 'Yes' : 'No',
        submitted_at:      new Date().toLocaleString(),
    };

    // Save to localStorage (same-device admin view)
    const stored = JSON.parse(localStorage.getItem(LS_KEY) || '[]');
    stored.push(entry);
    localStorage.setItem(LS_KEY, JSON.stringify(stored));

    // Submit to Google Sheets via Apps Script if configured.
    // Uses no-cors + FormData — the browser won't read the response,
    // but the Apps Script doPost() receives and saves all fields.
    if (GOOGLE_SCRIPT_URL !== 'YOUR_GOOGLE_SCRIPT_URL') {
        try {
            const fd = new FormData();
            Object.entries(entry).forEach(([k, v]) => fd.append(k, v));
            await fetch(GOOGLE_SCRIPT_URL, { method: 'POST', mode: 'no-cors', body: fd });
        } catch (err) {
            console.warn('Google Sheets error:', err);
        }
    }

    // Show success screen
    document.getElementById('form-card').style.display = 'none';
    document.querySelector('.tabs').style.display = 'none';
    const notice = document.getElementById('setup-notice');
    if (notice) notice.style.display = 'none';
    document.getElementById('success-msg').classList.add('visible');
    window.scrollTo({ top: 0, behavior: 'smooth' });
});

// ── Admin panel ───────────────────────────────────────────────────────────
function toggleAdmin() {
    const panel = document.getElementById('admin-panel');
    panel.classList.toggle('visible');
    if (panel.classList.contains('visible') && adminUnlocked) renderTable();
}

function checkAdminPass() {
    if (document.getElementById('admin-pass').value === ADMIN_PASSWORD) {
        adminUnlocked = true;
        document.getElementById('admin-login').style.display = 'none';
        document.getElementById('admin-content').style.display = 'block';
        renderTable();
    } else {
        document.getElementById('admin-err').style.display = 'block';
    }
}

function renderTable() {
    const data = JSON.parse(localStorage.getItem(LS_KEY) || '[]');
    document.getElementById('rsvp-count').textContent =
        data.length === 1 ? '1 entry' : `${data.length} entries`;

    const tbody = document.getElementById('rsvp-tbody');
    tbody.innerHTML = '';

    if (!data.length) {
        tbody.innerHTML = '<tr class="empty-row"><td colspan="10">No submissions on this device yet.</td></tr>';
        return;
    }

    data.forEach((r, i) => {
        const tr = document.createElement('tr');
        const intl = r.guest_type === 'International';
        tr.innerHTML = `
            <td>${i + 1}</td>
            <td><span class="badge ${intl ? 'badge-intl' : 'badge-local'}">${esc(r.guest_type)}</span></td>
            <td><strong>${esc(r.name)}</strong></td>
            <td>${esc(r.email)}</td>
            <td>${esc(r.mobile)}</td>
            <td>${esc(r.additional_guests || '—')}</td>
            <td>${esc(r.children || '—')}</td>
            <td>${esc(r.dietary || '—')}</td>
            <td>${r.whatsapp_consent === 'Yes' ? '✅ Yes' : '❌ No'}</td>
            <td style="white-space:nowrap; color:#999; font-size:.8em;">${esc(r.submitted_at)}</td>
        `;
        tbody.appendChild(tr);
    });
}

function esc(str) {
    return String(str ?? '').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

function exportCSV() {
    const data = JSON.parse(localStorage.getItem(LS_KEY) || '[]');
    if (!data.length) { alert('No data to export.'); return; }

    const headers = [
        '#', 'Type', 'Name', 'Email', 'Mobile',
        'Additional Guests', 'Children', 'Dietary / Allergies',
        'WhatsApp Consent', 'Submitted At'
    ];

    const rows = data.map((r, i) => [
        i + 1, r.guest_type, r.name, r.email, r.mobile,
        r.additional_guests || '', r.children || '',
        r.dietary || '', r.whatsapp_consent, r.submitted_at,
    ].map(v => `"${String(v).replace(/"/g, '""')}"`));

    const csv  = [headers.map(h => `"${h}"`), ...rows].map(r => r.join(',')).join('\r\n');
    const blob = new Blob(['﻿' + csv], { type: 'text/csv;charset=utf-8;' });
    const url  = URL.createObjectURL(blob);
    const a    = Object.assign(document.createElement('a'), {
        href: url, download: `rsvp_${new Date().toISOString().slice(0,10)}.csv`
    });
    a.click();
    URL.revokeObjectURL(url);
}

function clearData() {
    if (confirm('Delete all locally stored RSVP data? This cannot be undone.')) {
        localStorage.removeItem(LS_KEY);
        renderTable();
    }
}
</script>

</body>
</html>
