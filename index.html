import { useState, useRef, useCallback } from "react";

// â”€â”€â”€ Constants â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
const DEPOSIT_AMT = 5000;
const CHAIN_RATES = [0.25, 0.60, 0.015, 0.015];
const CHAIN_LABELS = ["à§§à¦® à¦†à¦ªà¦²à¦¾à¦‡à¦¨ (à§¨à§«%)", "à§¨à¦¯à¦¼ à¦†à¦ªà¦²à¦¾à¦‡à¦¨ (à§¬à§¦%)", "à§©à¦¯à¦¼ à¦†à¦ªà¦²à¦¾à¦‡à¦¨ (à§§.à§«%)", "à§ªà¦°à§à¦¥ à¦†à¦ªà¦²à¦¾à¦‡à¦¨ (à§§.à§«%)"];
const LEVEL_LABELS = { 0: "Admin", 1: "A", 2: "B", 3: "C", 4: "D", 5: "E" };
const LEVEL_COLORS = { 0: "#F59E0B", 1: "#6366F1", 2: "#10B981", 3: "#3B82F6", 4: "#EC4899", 5: "#8B5CF6" };

function genCode(name, id) { return (name || "MBR").replace(/\s+/g, "").toUpperCase().slice(0, 4) + id; }
let _nid = 20; const mkId = () => ++_nid;

// â”€â”€â”€ Initial Data â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
const mkNode = (id, name, level, parentId, phone, nid, password, children = []) => ({
  id, name, level, deposit: level === 0 ? 0 : DEPOSIT_AMT, parentId,
  referralCode: genCode(name, id), phone: phone || "", nid: nid || "",
  password: password || "", avatar: null, balance: 0, children,
});

const initTree = mkNode(1, "ADMIN", 0, null, "01700000000", "0000000000000", "admin123", [
  mkNode(2, "à¦¸à¦¦à¦¸à§à¦¯-A", 1, 1, "01711111111", "1234567890123", "pass123", [
    mkNode(3, "à¦¸à¦¦à¦¸à§à¦¯-B1", 2, 2, "01722222222", "2345678901234", "pass123", [
      mkNode(10, "à¦¸à¦¦à¦¸à§à¦¯-C1", 3, 3, "01744444444", "4567890123456", "pass123", []),
    ]),
    mkNode(4, "à¦¸à¦¦à¦¸à§à¦¯-B2", 2, 2, "01733333333", "3456789012345", "pass123", []),
  ]),
]);

// Initial payment agents
const initAgents = {
  bkash:  { name: "à¦¬à¦¿à¦•à¦¾à¦¶",  number: "01700000001" },
  nagad:  { name: "à¦¨à¦—à¦¦",    number: "01700000002" },
  rocket: { name: "à¦°à¦•à§‡à¦Ÿ",   number: "01700000003" },
};

// â”€â”€â”€ Helpers â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
function flatTree(node, arr = []) { arr.push(node); node.children.forEach(c => flatTree(c, arr)); return arr; }

function addToTree(tree, pid, n) {
  if (tree.id === pid) return { ...tree, children: [...tree.children, n] };
  return { ...tree, children: tree.children.map(c => addToTree(c, pid, n)) };
}

function updateInTree(tree, id, updater) {
  if (tree.id === id) return updater(tree);
  return { ...tree, children: tree.children.map(c => updateInTree(c, id, updater)) };
}

function removeFromTree(tree, tid) {
  return { ...tree, children: tree.children.filter(c => c.id !== tid).map(c => removeFromTree(c, tid)) };
}

// Get upline of a member (up to 4 levels)
function getUpline(allNodes, memberId) {
  const upline = [];
  let cur = allNodes.find(n => n.id === memberId);
  while (cur && upline.length < 4) {
    const parent = allNodes.find(n => n.id === cur.parentId);
    if (!parent) break;
    upline.push(parent);
    cur = parent;
  }
  return upline;
}

// Calculate total commission earned by a node
function calcComm(node, allNodes) {
  const descendants = flatTree(node).filter(n => n.id !== node.id && n.level > 0);
  let total = 0;
  const breakdown = [0, 0, 0, 0];
  descendants.forEach(member => {
    let cur = allNodes.find(n => n.id === member.parentId);
    let depth = 0;
    while (cur && depth < 4) {
      if (cur.id === node.id) {
        const amt = DEPOSIT_AMT * CHAIN_RATES[depth];
        breakdown[depth] += amt; total += amt; break;
      }
      cur = allNodes.find(n => n.id === cur.parentId);
      depth++;
    }
  });
  const lvls = CHAIN_RATES.map((rate, i) => ({ rate, amt: breakdown[i], count: breakdown[i] > 0 ? Math.round(breakdown[i] / (DEPOSIT_AMT * rate)) : 0 }));
  return { lvls, total };
}

// â”€â”€â”€ Shared UI Components â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
const inputStyle = (extra = {}) => ({
  width: "100%", padding: "11px 14px", borderRadius: 10, boxSizing: "border-box",
  background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.1)",
  color: "#E2E8F0", fontSize: 13, fontFamily: "'Hind Siliguri',sans-serif", outline: "none", ...extra
});

function TxtInp({ label, value, onChange, placeholder, type = "text", note, required, disabled }) {
  return (
    <div style={{ marginBottom: 13 }}>
      {label && <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>{label}{required && <span style={{ color: "#F87171" }}> *</span>}</label>}
      <input type={type} value={value} onChange={e => onChange(e.target.value)} placeholder={placeholder} disabled={disabled}
        style={inputStyle({ opacity: disabled ? 0.5 : 1 })}
        onFocus={e => { if (!disabled) e.target.style.borderColor = "rgba(99,102,241,0.6)"; }}
        onBlur={e => e.target.style.borderColor = "rgba(255,255,255,0.1)"} />
      {note && <div style={{ fontSize: 10, color: "#475569", marginTop: 4 }}>{note}</div>}
    </div>
  );
}

function PwInp({ label, value, onChange, placeholder, required, showToggle = true, alwaysShow = false }) {
  const [show, setShow] = useState(alwaysShow);
  return (
    <div style={{ marginBottom: 13 }}>
      {label && <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>{label}{required && <span style={{ color: "#F87171" }}> *</span>}</label>}
      <div style={{ position: "relative" }}>
        <input type={show ? "text" : "password"} value={value} onChange={e => onChange(e.target.value)} placeholder={placeholder}
          style={inputStyle({ paddingRight: showToggle ? 44 : 14 })}
          onFocus={e => e.target.style.borderColor = "rgba(99,102,241,0.6)"}
          onBlur={e => e.target.style.borderColor = "rgba(255,255,255,0.1)"} />
        {showToggle && <button onClick={() => setShow(s => !s)} style={{ position: "absolute", right: 12, top: "50%", transform: "translateY(-50%)", background: "none", border: "none", cursor: "pointer", fontSize: 15, color: "#64748B", padding: 0 }}>{show ? "ðŸ™ˆ" : "ðŸ‘ï¸"}</button>}
      </div>
    </div>
  );
}

function Flash({ m }) {
  if (!m) return null;
  const ok = m.startsWith("âœ…"), warn = m.startsWith("âš ï¸");
  return <div style={{ background: ok ? "rgba(16,185,129,0.12)" : warn ? "rgba(245,158,11,0.12)" : "rgba(239,68,68,0.12)", border: `1px solid ${ok ? "rgba(16,185,129,0.3)" : warn ? "rgba(245,158,11,0.3)" : "rgba(239,68,68,0.3)"}`, borderRadius: 10, padding: "10px 14px", marginBottom: 13, fontSize: 12, color: ok ? "#34D399" : warn ? "#FCD34D" : "#F87171" }}>{m}</div>;
}

function Btn({ children, onClick, color = "indigo", disabled, small }) {
  const bg = { indigo: "linear-gradient(135deg,#6366F1,#8B5CF6)", green: "linear-gradient(135deg,#10B981,#059669)", red: "linear-gradient(135deg,#EF4444,#DC2626)", amber: "linear-gradient(135deg,#F59E0B,#D97706)", gray: "rgba(255,255,255,0.08)" }[color];
  return <button onClick={onClick} disabled={disabled} style={{ background: disabled ? "rgba(255,255,255,0.05)" : bg, border: "none", borderRadius: small ? 8 : 11, color: disabled ? "#374151" : "#fff", padding: small ? "7px 14px" : "13px 20px", fontSize: small ? 12 : 14, fontWeight: 700, fontFamily: "'Hind Siliguri',sans-serif", cursor: disabled ? "not-allowed" : "pointer", width: small ? "auto" : "100%", transition: "opacity 0.2s" }}>{children}</button>;
}

function SectionTitle({ icon, title }) {
  return <div style={{ fontSize: 12, fontWeight: 700, color: "#A78BFA", marginBottom: 13, paddingBottom: 8, borderBottom: "1px solid rgba(255,255,255,0.06)", display: "flex", alignItems: "center", gap: 6 }}><span style={{ fontSize: 16 }}>{icon}</span>{title}</div>;
}

// â”€â”€â”€ Avatar Component â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
function Avatar({ node, size = 56, editable = false, onUpload }) {
  const ref = useRef();
  const col = LEVEL_COLORS[Math.min(node.level, 5)];
  const handleFile = (e) => {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = (ev) => onUpload && onUpload(ev.target.result);
    reader.readAsDataURL(file);
  };
  return (
    <div style={{ position: "relative", width: size, height: size, flexShrink: 0 }}>
      <div style={{ width: size, height: size, borderRadius: "50%", background: node.avatar ? "transparent" : `linear-gradient(135deg,${col},${col}99)`, border: `3px solid ${col}55`, overflow: "hidden", display: "flex", alignItems: "center", justifyContent: "center" }}>
        {node.avatar ? <img src={node.avatar} alt="avatar" style={{ width: "100%", height: "100%", objectFit: "cover" }} /> : <span style={{ fontSize: size * 0.38, fontWeight: 700, color: "#fff" }}>{(node.name || "?")[0]}</span>}
      </div>
      {editable && (
        <>
          <div onClick={() => ref.current.click()} style={{ position: "absolute", bottom: 0, right: 0, width: 22, height: 22, borderRadius: "50%", background: "#6366F1", border: "2px solid #080812", display: "flex", alignItems: "center", justifyContent: "center", cursor: "pointer", fontSize: 11 }}>ðŸ“·</div>
          <input ref={ref} type="file" accept="image/*" onChange={handleFile} style={{ display: "none" }} />
        </>
      )}
    </div>
  );
}


// â”€â”€â”€ Agent Selector (Accordion) â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
function AgentSelector({ agents, onCopy }) {
  const [selected, setSelected] = useState(null);
  const icons = { bkash: "ðŸ’—", nagad: "ðŸŸ ", rocket: "ðŸš€" };
  const colors = { bkash: "#E2136E", nagad: "#F26522", rocket: "#8B5CF6" };

  return (
    <div style={{ marginBottom: 4 }}>
      {Object.entries(agents).map(([key, ag]) => {
        const isOpen = selected === key;
        const col = colors[key];
        return (
          <div key={key} style={{ marginBottom: 8, borderRadius: 12, overflow: "hidden", border: `1px solid ${isOpen ? col + "55" : "rgba(255,255,255,0.07)"}`, transition: "all 0.2s" }}>
            {/* Header - click to toggle */}
            <div
              onClick={() => setSelected(isOpen ? null : key)}
              style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "13px 15px", background: isOpen ? col + "18" : "rgba(255,255,255,0.03)", cursor: "pointer", userSelect: "none" }}
            >
              <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                <div style={{ width: 38, height: 38, borderRadius: 10, background: col + "25", border: `1.5px solid ${col}44`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 20 }}>{icons[key]}</div>
                <div>
                  <div style={{ fontSize: 13, fontWeight: 700, color: "#E2E8F0" }}>{ag.name}</div>
                  <div style={{ fontSize: 10, color: "#64748B" }}>à¦•à§à¦²à¦¿à¦• à¦•à¦°à§à¦¨ à¦¨à¦®à§à¦¬à¦° à¦¦à§‡à¦–à¦¤à§‡</div>
                </div>
              </div>
              <div style={{ fontSize: 18, color: isOpen ? col : "#374151", transition: "transform 0.2s", transform: isOpen ? "rotate(180deg)" : "rotate(0deg)" }}>âŒ„</div>
            </div>

            {/* Dropdown - number + copy */}
            {isOpen && (
              <div style={{ padding: "14px 15px", background: "rgba(0,0,0,0.25)", borderTop: `1px solid ${col}33` }}>
                <div style={{ fontSize: 11, color: "#64748B", marginBottom: 6 }}>{ag.name} à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¨à¦®à§à¦¬à¦°:</div>
                <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", background: col + "12", borderRadius: 10, padding: "12px 14px", border: `1px solid ${col}33` }}>
                  <span style={{ fontSize: 20, fontWeight: 700, color: col, letterSpacing: 2 }}>{ag.number}</span>
                  <button
                    onClick={() => onCopy(ag.number)}
                    style={{ background: col + "25", border: `1px solid ${col}55`, color: col, borderRadius: 8, padding: "7px 14px", cursor: "pointer", fontSize: 12, fontFamily: "'Hind Siliguri',sans-serif", fontWeight: 700 }}
                  >ðŸ“‹ à¦•à¦ªà¦¿</button>
                </div>
                <div style={{ fontSize: 10, color: "#475569", marginTop: 8 }}>
                  âš ï¸ à¦à¦‡ à¦¨à¦®à§à¦¬à¦°à§‡ à¦Ÿà¦¾à¦•à¦¾ à¦ªà¦¾à¦ à¦¿à¦¯à¦¼à§‡ à¦¨à¦¿à¦šà§‡ à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦†à¦‡à¦¡à¦¿ à¦¸à¦¾à¦¬à¦®à¦¿à¦Ÿ à¦•à¦°à§à¦¨
                </div>
              </div>
            )}
          </div>
        );
      })}
    </div>
  );
}

// â”€â”€â”€ Tree Node â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
function TreeNode({ node, onSelect, selId }) {
  const [exp, setExp] = useState(true);
  const sel = node.id === selId;
  const col = LEVEL_COLORS[Math.min(node.level, 5)];
  const has = node.children.length > 0;
  return (
    <div style={{ display: "flex", flexDirection: "column", alignItems: "center" }}>
      <div onClick={() => { onSelect(node); if (has) setExp(e => !e); }} style={{ background: sel ? `linear-gradient(135deg,${col},${col}bb)` : "rgba(255,255,255,0.04)", border: `2px solid ${sel ? col : col + "44"}`, borderRadius: 10, padding: "7px 12px", minWidth: 76, textAlign: "center", cursor: "pointer", position: "relative", boxShadow: sel ? `0 0 14px ${col}55` : "none", userSelect: "none", transition: "all 0.2s" }}>
        <div style={{ color: sel ? "#fff" : col, fontSize: 10, fontWeight: 700 }}>{node.name}</div>
        <div style={{ color: "rgba(255,255,255,0.3)", fontSize: 8, marginTop: 1 }}>#{node.id} Lv{node.level}</div>
        {has && <div style={{ position: "absolute", bottom: -7, left: "50%", transform: "translateX(-50%)", width: 14, height: 14, borderRadius: "50%", background: col, color: "#fff", fontSize: 9, display: "flex", alignItems: "center", justifyContent: "center", fontWeight: 700 }}>{exp ? "âˆ’" : "+"}</div>}
      </div>
      {has && exp && (
        <>
          <div style={{ width: 2, height: 16, background: `${col}33` }} />
          <div style={{ display: "flex", alignItems: "flex-start" }}>
            {node.children.map(child => (
              <div key={child.id} style={{ display: "flex", flexDirection: "column", alignItems: "center", padding: "0 4px" }}>
                <div style={{ width: 2, height: 16, background: `${LEVEL_COLORS[Math.min(child.level, 5)]}33` }} />
                <TreeNode node={child} onSelect={onSelect} selId={selId} />
              </div>
            ))}
          </div>
        </>
      )}
    </div>
  );
}

// â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
// MAIN APP
// â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
export default function App() {
  const [screen, setScreen] = useState("login");
  const [tree, setTree] = useState(initTree);
  const [agents, setAgents] = useState(initAgents);
  const [transactions, setTransactions] = useState([]); // global tx list
  const [tab, setTab] = useState("profile");
  const [adminTab, setAdminTab] = useState("users");
  const [user, setUser] = useState(null);
  const [msg, setMsg] = useState("");
  const [selNode, setSelNode] = useState(null);

  // Forms
  const [loginId, setLoginId] = useState(""); const [loginPw, setLoginPw] = useState("");
  const [reg, setReg] = useState({ name: "", phone: "", nid: "", refCode: "", password: "", confirmPw: "" });
  const [fp, setFp] = useState({ step: 1, phone: "", nid: "", newPw: "", confirm: "", foundUser: null });
  const [depForm, setDepForm] = useState({ method: "bkash", txId: "", phone: "", amount: DEPOSIT_AMT });
  const [adminEdit, setAdminEdit] = useState(null); // user being edited in admin
  const [adminMsg, setAdminMsg] = useState("");

  const flash = (m, dur = 3500) => { setMsg(m); if (dur > 0) setTimeout(() => setMsg(""), dur); };
  const aFlash = (m, dur = 3500) => { setAdminMsg(m); if (dur > 0) setTimeout(() => setAdminMsg(""), dur); };
  const all = flatTree(tree);
  const members = all.filter(n => n.level > 0);
  const isAdmin = user?.level === 0;

  const refNode = reg.refCode.trim() ? all.find(n => n.referralCode === reg.refCode.trim().toUpperCase()) : null;
  const refEmpty = reg.refCode.trim() === "";
  const refValid = refEmpty || !!refNode;

  // â”€â”€ Tree updater helpers â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const updateUser = useCallback((id, updater) => {
    setTree(prev => updateInTree(prev, id, updater));
    if (user?.id === id) setUser(prev => updater(prev));
  }, [user]);

  // â”€â”€ Distribute commission to upline â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const distributeCommission = (memberId, depositAmt) => {
    const upline = getUpline(all, memberId);
    upline.forEach((upNode, i) => {
      if (i >= CHAIN_RATES.length) return;
      const commAmt = depositAmt * CHAIN_RATES[i];
      setTree(prev => updateInTree(prev, upNode.id, n => ({ ...n, balance: (n.balance || 0) + commAmt })));
      if (user?.id === upNode.id) setUser(prev => ({ ...prev, balance: (prev.balance || 0) + commAmt }));
      // log tx for upline
      setTransactions(prev => [...prev, {
        id: mkId(), type: "commission", memberId, uplineId: upNode.id,
        amount: commAmt, rate: `${CHAIN_RATES[i] * 100}%`, depth: i + 1,
        date: new Date().toLocaleDateString("bn-BD"), status: "confirmed"
      }]);
    });
    // remaining goes to admin
    const totalComm = CHAIN_RATES.reduce((s, r) => s + depositAmt * r, 0);
    const adminShare = depositAmt - totalComm;
    setTree(prev => updateInTree(prev, 1, n => ({ ...n, balance: (n.balance || 0) + adminShare })));
  };

  // â”€â”€ Login â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doLogin = () => {
    const id = loginId.trim(), pw = loginPw.trim();
    if (!id || !pw) { flash("âŒ à¦¸à¦¬ à¦¤à¦¥à§à¦¯ à¦ªà§‚à¦°à¦£ à¦•à¦°à§à¦¨"); return; }
    const found = all.find(n => (n.referralCode === id.toUpperCase() || n.phone === id || n.name === id) && n.password === pw);
    if (!found) { flash("âŒ à¦‡à¦‰à¦œà¦¾à¦°à¦¨à§‡à¦®/à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¬à¦¾ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦¸à¦ à¦¿à¦• à¦¨à¦¯à¦¼"); return; }
    setUser(found); setLoginId(""); setLoginPw(""); setMsg("");
    setScreen(found.level === 0 ? "admin" : "app");
    setTab("profile"); setAdminTab("users");
  };

  // â”€â”€ Register â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doRegister = () => {
    const { name, phone, nid, refCode, password, confirmPw } = reg;
    if (!name.trim() || !phone.trim() || !nid.trim() || !password.trim()) { flash("âŒ à¦¸à¦¬ à¦¤à¦¥à§à¦¯ à¦ªà§‚à¦°à¦£ à¦•à¦°à§à¦¨"); return; }
    if (phone.length < 11) { flash("âŒ à¦¸à¦ à¦¿à¦• à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦° à¦¦à¦¿à¦¨"); return; }
    if (nid.length < 10) { flash("âŒ à¦¸à¦ à¦¿à¦• NID à¦¨à¦®à§à¦¬à¦° à¦¦à¦¿à¦¨"); return; }
    if (password.length < 6) { flash("âŒ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦•à¦®à¦ªà¦•à§à¦·à§‡ à§¬ à¦…à¦•à§à¦·à¦°"); return; }
    if (password !== confirmPw) { flash("âŒ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦®à¦¿à¦²à¦›à§‡ à¦¨à¦¾"); return; }
    if (all.find(n => n.phone === phone.trim())) { flash("âŒ à¦à¦‡ à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦°à§‡ à¦…à§à¦¯à¦¾à¦•à¦¾à¦‰à¦¨à§à¦Ÿ à¦†à¦›à§‡"); return; }
    if (all.find(n => n.nid === nid.trim())) { flash("âŒ à¦à¦‡ NID à¦¤à§‡ à¦…à§à¦¯à¦¾à¦•à¦¾à¦‰à¦¨à§à¦Ÿ à¦†à¦›à§‡"); return; }
    let parent = all.find(n => n.id === 1);
    if (refCode.trim()) {
      const found = all.find(n => n.referralCode === refCode.trim().toUpperCase());
      if (!found) { flash("âŒ à¦°à§‡à¦«à¦¾à¦° à¦•à§‹à¦¡ à¦¸à¦ à¦¿à¦• à¦¨à¦¯à¦¼"); return; }
      if (found.level >= 5) { flash("âŒ à¦¸à¦°à§à¦¬à§‹à¦šà§à¦š à¦²à§‡à¦­à§‡à¦² à¦ªà¦¾à¦° à¦•à¦°à¦¾ à¦¯à¦¾à¦¬à§‡ à¦¨à¦¾"); return; }
      parent = found;
    }
    const newId = mkId();
    const newMember = { id: newId, name: name.trim(), level: parent.level + 1, deposit: DEPOSIT_AMT, parentId: parent.id, referralCode: genCode(name.trim(), newId), phone: phone.trim(), nid: nid.trim(), password, avatar: null, balance: 0, children: [] };
    setTree(prev => addToTree(prev, parent.id, newMember));
    setUser(newMember); setReg({ name: "", phone: "", nid: "", refCode: "", password: "", confirmPw: "" });
    setScreen("app"); setTab("profile"); setMsg("");
  };

  // â”€â”€ Forgot Password â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doFpVerify = () => {
    const found = all.find(n => n.phone === fp.phone.trim() && n.nid === fp.nid.trim());
    if (!found) { flash("âŒ à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¬à¦¾ NID à¦¨à¦®à§à¦¬à¦° à¦®à¦¿à¦²à¦›à§‡ à¦¨à¦¾"); return; }
    setFp(f => ({ ...f, step: 2, foundUser: found })); setMsg("");
  };
  const doFpReset = () => {
    if (!fp.newPw || fp.newPw.length < 6) { flash("âŒ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦•à¦®à¦ªà¦•à§à¦·à§‡ à§¬ à¦…à¦•à§à¦·à¦°"); return; }
    if (fp.newPw !== fp.confirm) { flash("âŒ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦®à¦¿à¦²à¦›à§‡ à¦¨à¦¾"); return; }
    setTree(prev => updateInTree(prev, fp.foundUser.id, n => ({ ...n, password: fp.newPw })));
    flash("âœ… à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦ªà¦°à¦¿à¦¬à¦°à§à¦¤à¦¨ à¦¸à¦«à¦²!");
    setTimeout(() => { setScreen("login"); setFp({ step: 1, phone: "", nid: "", newPw: "", confirm: "", foundUser: null }); setMsg(""); }, 1800);
  };

  // â”€â”€ Deposit submission â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doSubmitDeposit = () => {
    if (!depForm.txId.trim()) { flash("âŒ à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦†à¦‡à¦¡à¦¿ à¦¦à¦¿à¦¨"); return; }
    if (!depForm.phone.trim() || depForm.phone.length < 11) { flash("âŒ à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦° à¦¦à¦¿à¦¨"); return; }
    if (transactions.find(t => t.txId === depForm.txId.trim())) { flash("âŒ à¦à¦‡ à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦†à¦‡à¦¡à¦¿ à¦†à¦—à§‡à¦‡ à¦¬à§à¦¯à¦¬à¦¹à§ƒà¦¤ à¦¹à¦¯à¦¼à§‡à¦›à§‡"); return; }
    const tx = {
      id: mkId(), txId: depForm.txId.trim(), memberId: user.id,
      memberName: user.name, method: depForm.method,
      senderPhone: depForm.phone.trim(), amount: depForm.amount,
      date: new Date().toLocaleDateString("bn-BD"),
      status: "pending", type: "deposit",
    };
    setTransactions(prev => [...prev, tx]);
    flash("âœ… à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ à¦¸à¦¾à¦¬à¦®à¦¿à¦Ÿ à¦¹à¦¯à¦¼à§‡à¦›à§‡! à¦…à§à¦¯à¦¾à¦¡à¦®à¦¿à¦¨ à¦­à§‡à¦°à¦¿à¦«à¦¾à¦‡ à¦•à¦°à¦²à§‡ à¦•à¦®à¦¿à¦¶à¦¨ à¦¬à¦¿à¦¤à¦°à¦£ à¦¹à¦¬à§‡à¥¤");
    setDepForm({ method: "bkash", txId: "", phone: "", amount: DEPOSIT_AMT });
  };

  // â”€â”€ Admin: verify deposit â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doVerifyDeposit = (txId) => {
    const tx = transactions.find(t => t.id === txId);
    if (!tx || tx.status === "confirmed") return;
    setTransactions(prev => prev.map(t => t.id === txId ? { ...t, status: "confirmed" } : t));
    distributeCommission(tx.memberId, tx.amount);
    aFlash(`âœ… à§³${tx.amount.toLocaleString()} à¦­à§‡à¦°à¦¿à¦«à¦¾à¦‡ à¦¸à¦®à§à¦ªà¦¨à§à¦¨! à¦•à¦®à¦¿à¦¶à¦¨ à¦¬à¦¿à¦¤à¦°à¦£ à¦¹à¦¯à¦¼à§‡à¦›à§‡à¥¤`);
  };

  // â”€â”€ Admin: edit user â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€
  const doSaveUser = () => {
    if (!adminEdit) return;
    updateUser(adminEdit.id, () => ({ ...adminEdit }));
    aFlash("âœ… à¦¤à¦¥à§à¦¯ à¦¸à¦«à¦²à¦­à¦¾à¦¬à§‡ à¦†à¦ªà¦¡à§‡à¦Ÿ à¦¹à¦¯à¦¼à§‡à¦›à§‡!");
    setAdminEdit(null);
  };

  const BG = () => (
    <>
      <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet" />
      <div style={{ position: "fixed", inset: 0, pointerEvents: "none", zIndex: 0 }}>
        <div style={{ position: "absolute", top: -80, left: -80, width: 350, height: 350, background: "radial-gradient(circle,rgba(99,102,241,0.15) 0%,transparent 65%)" }} />
        <div style={{ position: "absolute", bottom: -80, right: -80, width: 300, height: 300, background: "radial-gradient(circle,rgba(245,158,11,0.10) 0%,transparent 65%)" }} />
      </div>
    </>
  );

  const wrap = (content) => (
    <div style={{ minHeight: "100vh", background: "#080812", fontFamily: "'Hind Siliguri','Segoe UI',sans-serif", color: "#E2E8F0" }}>
      <BG />
      <div style={{ position: "relative", zIndex: 1, maxWidth: 420, margin: "0 auto" }}>{content}</div>
    </div>
  );

  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  // LOGIN
  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  if (screen === "login") return wrap(
    <div style={{ minHeight: "100vh", display: "flex", justifyContent: "center", alignItems: "center", padding: "0 22px" }}>
      <div style={{ width: "100%" }}>
        <div style={{ textAlign: "center", marginBottom: 30 }}>
          <div style={{ width: 70, height: 70, borderRadius: 20, margin: "0 auto 12px", background: "linear-gradient(135deg,#6366F1,#F59E0B)", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 30, boxShadow: "0 8px 28px rgba(99,102,241,0.4)" }}>ðŸŒ</div>
          <div style={{ fontSize: 26, fontWeight: 700, color: "#F59E0B", letterSpacing: 2 }}>RSM LIFE</div>
          <div style={{ fontSize: 11, color: "#475569", marginTop: 3 }}>RSM LIFE â€” à¦†à¦ªà¦¨à¦¾à¦° à¦¸à¦¾à¦«à¦²à§à¦¯à§‡à¦° à¦ªà¦¥</div>
        </div>
        <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 20, padding: "26px 22px", border: "1px solid rgba(255,255,255,0.07)" }}>
          <div style={{ fontSize: 17, fontWeight: 700, color: "#E2E8F0", marginBottom: 18 }}>à¦¸à§à¦¬à¦¾à¦—à¦¤à¦® ðŸ‘‹</div>
          <Flash m={msg} />
          <TxtInp label="à¦‡à¦‰à¦œà¦¾à¦°à¦¨à§‡à¦® / à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦°" value={loginId} onChange={setLoginId} placeholder="à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¬à¦¾ à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡" required />
          <div style={{ marginBottom: 14 }}>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 5 }}>
              <label style={{ fontSize: 12, color: "#94A3B8" }}>à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ <span style={{ color: "#F87171" }}>*</span></label>
              <button onClick={() => { setScreen("forgot"); setMsg(""); }} style={{ background: "none", border: "none", color: "#6366F1", fontSize: 11, fontWeight: 600, cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif", padding: 0 }}>à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦­à§à¦²à§‡ à¦—à§‡à¦›à§‡à¦¨?</button>
            </div>
            <PwInp value={loginPw} onChange={setLoginPw} placeholder="à¦†à¦ªà¦¨à¦¾à¦° à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" required />
          </div>
          <Btn onClick={doLogin} color="indigo">à¦²à¦—à¦‡à¦¨ à¦•à¦°à§à¦¨ â†’</Btn>
          <div style={{ textAlign: "center", marginTop: 14 }}>
            <span style={{ fontSize: 12, color: "#475569" }}>à¦¨à¦¤à§à¦¨? </span>
            <button onClick={() => { setScreen("register"); setMsg(""); }} style={{ background: "none", border: "none", color: "#6366F1", fontSize: 12, fontWeight: 700, cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif" }}>à¦°à§‡à¦œà¦¿à¦¸à§à¦Ÿà§à¦°à§‡à¦¶à¦¨ à¦•à¦°à§à¦¨</button>
          </div>
        </div>
        <div style={{ marginTop: 12, background: "rgba(245,158,11,0.07)", borderRadius: 11, padding: "11px 14px", border: "1px solid rgba(245,158,11,0.15)" }}>
          <div style={{ fontSize: 11, color: "#FCD34D", marginBottom: 4, fontWeight: 600 }}>ðŸ”‘ à¦¡à§‡à¦®à§‹</div>
          <div style={{ fontSize: 11, color: "#64748B" }}>à¦…à§à¦¯à¦¾à¦¡à¦®à¦¿à¦¨: <span style={{ color: "#F59E0B" }}>01700000000</span> / <span style={{ color: "#F59E0B" }}>admin123</span></div>
          <div style={{ fontSize: 11, color: "#64748B" }}>à¦¸à¦¦à¦¸à§à¦¯: <span style={{ color: "#10B981" }}>01711111111</span> / <span style={{ color: "#10B981" }}>pass123</span></div>
        </div>
      </div>
    </div>
  );

  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  // FORGOT PASSWORD
  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  if (screen === "forgot") return wrap(
    <div style={{ padding: "28px 22px 60px" }}>
      <div style={{ display: "flex", alignItems: "center", marginBottom: 24 }}>
        <button onClick={() => { setScreen("login"); setMsg(""); setFp({ step: 1, phone: "", nid: "", newPw: "", confirm: "", foundUser: null }); }} style={{ background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.1)", color: "#94A3B8", borderRadius: 9, width: 34, height: 34, cursor: "pointer", fontSize: 15, display: "flex", alignItems: "center", justifyContent: "center" }}>â†</button>
        <div style={{ marginLeft: 10 }}><div style={{ fontSize: 17, fontWeight: 700, color: "#E2E8F0" }}>à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦°à¦¿à¦¸à§‡à¦Ÿ</div><div style={{ fontSize: 11, color: "#475569" }}>{fp.step === 1 ? "à¦ªà¦°à¦¿à¦šà¦¯à¦¼ à¦¯à¦¾à¦šà¦¾à¦‡ à¦•à¦°à§à¦¨" : `à¦¸à§à¦¬à¦¾à¦—à¦¤à¦®, ${fp.foundUser?.name}`}</div></div>
      </div>
      <div style={{ display: "flex", gap: 8, marginBottom: 20 }}>
        {[1, 2].map(s => <div key={s} style={{ flex: 1, height: 4, borderRadius: 4, background: s <= fp.step ? "linear-gradient(90deg,#6366F1,#8B5CF6)" : "rgba(255,255,255,0.08)" }} />)}
      </div>
      <Flash m={msg} />
      <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 18, padding: "22px", border: "1px solid rgba(255,255,255,0.07)" }}>
        {fp.step === 1 ? (
          <>
            <div style={{ textAlign: "center", marginBottom: 18 }}><div style={{ fontSize: 34, marginBottom: 8 }}>ðŸ”</div><div style={{ fontSize: 13, fontWeight: 700, color: "#E2E8F0" }}>à¦ªà¦°à¦¿à¦šà¦¯à¦¼ à¦¯à¦¾à¦šà¦¾à¦‡</div></div>
            <TxtInp label="à¦¨à¦¿à¦¬à¦¨à§à¦§à¦¿à¦¤ à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦°" value={fp.phone} onChange={v => setFp(f => ({ ...f, phone: v }))} placeholder="01XXXXXXXXX" type="tel" required />
            <TxtInp label="NID à¦¨à¦®à§à¦¬à¦°" value={fp.nid} onChange={v => setFp(f => ({ ...f, nid: v }))} placeholder="NID à¦¨à¦®à§à¦¬à¦°" type="number" required />
            <Btn onClick={doFpVerify} color="indigo">à¦ªà¦°à¦¿à¦šà¦¯à¦¼ à¦¯à¦¾à¦šà¦¾à¦‡ à¦•à¦°à§à¦¨ â†’</Btn>
          </>
        ) : (
          <>
            <div style={{ background: "rgba(16,185,129,0.08)", borderRadius: 10, padding: "11px 13px", marginBottom: 16, border: "1px solid rgba(16,185,129,0.2)", display: "flex", alignItems: "center", gap: 10 }}>
              <Avatar node={fp.foundUser} size={38} />
              <div><div style={{ fontSize: 13, fontWeight: 700, color: "#34D399" }}>âœ… {fp.foundUser?.name}</div><div style={{ fontSize: 10, color: "#065F46" }}>ðŸ“± {fp.foundUser?.phone}</div></div>
            </div>
            <PwInp label="à¦¨à¦¤à§à¦¨ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" value={fp.newPw} onChange={v => setFp(f => ({ ...f, newPw: v }))} placeholder="à¦•à¦®à¦ªà¦•à§à¦·à§‡ à§¬ à¦…à¦•à§à¦·à¦°" required />
            <div style={{ marginBottom: 14 }}>
              <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>à¦•à¦¨à¦«à¦¾à¦°à§à¦® à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ *</label>
              <div style={{ position: "relative" }}><input type="password" value={fp.confirm} onChange={e => setFp(f => ({ ...f, confirm: e.target.value }))} placeholder="à¦ªà§à¦¨à¦°à¦¾à¦¯à¦¼ à¦²à¦¿à¦–à§à¦¨" style={inputStyle({ paddingRight: 44 })} />{fp.confirm && <div style={{ position: "absolute", right: 12, top: "50%", transform: "translateY(-50%)", fontSize: 14 }}>{fp.newPw === fp.confirm ? "âœ…" : "âŒ"}</div>}</div>
            </div>
            <Btn onClick={doFpReset} color="green">âœ… à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦ªà¦°à¦¿à¦¬à¦°à§à¦¤à¦¨ à¦•à¦°à§à¦¨</Btn>
          </>
        )}
      </div>
    </div>
  );

  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  // REGISTER
  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  if (screen === "register") return wrap(
    <div style={{ padding: "24px 22px 80px" }}>
      <div style={{ display: "flex", alignItems: "center", marginBottom: 20 }}>
        <button onClick={() => { setScreen("login"); setMsg(""); }} style={{ background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.1)", color: "#94A3B8", borderRadius: 9, width: 34, height: 34, cursor: "pointer", fontSize: 15, display: "flex", alignItems: "center", justifyContent: "center" }}>â†</button>
        <div style={{ marginLeft: 10 }}><div style={{ fontSize: 17, fontWeight: 700, color: "#E2E8F0" }}>à¦¨à¦¤à§à¦¨ à¦…à§à¦¯à¦¾à¦•à¦¾à¦‰à¦¨à§à¦Ÿ</div><div style={{ fontSize: 11, color: "#475569" }}>RSM LIFE à¦¸à¦¦à¦¸à§à¦¯ à¦¹à¦¿à¦¸à§‡à¦¬à§‡ à¦¯à§‹à¦— à¦¦à¦¿à¦¨</div></div>
      </div>
      <div style={{ borderRadius: 12, padding: "12px 14px", marginBottom: 16, background: refEmpty ? "rgba(245,158,11,0.08)" : refNode ? "rgba(16,185,129,0.08)" : "rgba(239,68,68,0.08)", border: `1px solid ${refEmpty ? "rgba(245,158,11,0.2)" : refNode ? "rgba(16,185,129,0.25)" : "rgba(239,68,68,0.25)"}` }}>
        {refEmpty ? <div style={{ fontSize: 11, color: "#FCD34D" }}>â„¹ï¸ à¦°à§‡à¦«à¦¾à¦° à¦•à§‹à¦¡ à¦›à¦¾à¦¡à¦¼à¦¾ â†’ à¦¸à¦°à¦¾à¦¸à¦°à¦¿ <b style={{ color: "#F59E0B" }}>ADMIN</b> à¦à¦° à¦…à¦§à§€à¦¨à§‡</div> : refNode ? <div style={{ fontSize: 11, color: "#34D399" }}>âœ… à¦°à§‡à¦«à¦¾à¦°à¦¾à¦°: <b style={{ color: "#10B981" }}>{refNode.name}</b> â†’ à¦²à§‡à¦­à§‡à¦² {refNode.level + 1}</div> : <div style={{ fontSize: 11, color: "#F87171" }}>âŒ à¦°à§‡à¦«à¦¾à¦° à¦•à§‹à¦¡ à¦¸à¦ à¦¿à¦• à¦¨à¦¯à¦¼</div>}
      </div>
      <Flash m={msg} />
      <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 18, padding: "20px", border: "1px solid rgba(255,255,255,0.07)" }}>
        <SectionTitle icon="ðŸ‘¤" title="à¦¬à§à¦¯à¦•à§à¦¤à¦¿à¦—à¦¤ à¦¤à¦¥à§à¦¯" />
        <TxtInp label="à¦ªà§à¦°à§‹ à¦¨à¦¾à¦®" value={reg.name} onChange={v => setReg(f => ({ ...f, name: v }))} placeholder="à¦†à¦ªà¦¨à¦¾à¦° à¦ªà§à¦°à§‹ à¦¨à¦¾à¦®" required />
        <TxtInp label="à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦°" value={reg.phone} onChange={v => setReg(f => ({ ...f, phone: v }))} placeholder="01XXXXXXXXX" type="tel" required note="à¦à¦‡ à¦¨à¦®à§à¦¬à¦° à¦¦à¦¿à¦¯à¦¼à§‡ à¦²à¦—à¦‡à¦¨ à¦•à¦°à¦¤à§‡ à¦ªà¦¾à¦°à¦¬à§‡à¦¨" />
        <TxtInp label="NID à¦¨à¦®à§à¦¬à¦°" value={reg.nid} onChange={v => setReg(f => ({ ...f, nid: v }))} placeholder="à§§à§¦ à¦¬à¦¾ à§§à§© à¦¡à¦¿à¦œà¦¿à¦Ÿ" type="number" required />
        <SectionTitle icon="ðŸ”—" title="à¦°à§‡à¦«à¦¾à¦°à§‡à¦²" />
        <div style={{ marginBottom: 16 }}>
          <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡ (à¦à¦šà§à¦›à¦¿à¦•)</label>
          <input type="text" value={reg.refCode} onChange={e => setReg(f => ({ ...f, refCode: e.target.value }))} placeholder="à¦°à§‡à¦«à¦¾à¦° à¦•à§‹à¦¡ à¦¨à¦¾ à¦¥à¦¾à¦•à¦²à§‡ à¦–à¦¾à¦²à¦¿" style={inputStyle({ border: `1px solid ${refEmpty ? "rgba(255,255,255,0.1)" : refNode ? "rgba(16,185,129,0.5)" : "rgba(239,68,68,0.5)"}` })} />
        </div>
        <SectionTitle icon="ðŸ”’" title="à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" />
        <PwInp label="à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" value={reg.password} onChange={v => setReg(f => ({ ...f, password: v }))} placeholder="à¦•à¦®à¦ªà¦•à§à¦·à§‡ à§¬ à¦…à¦•à§à¦·à¦°" required />
        <div style={{ marginBottom: 18 }}>
          <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>à¦•à¦¨à¦«à¦¾à¦°à§à¦® à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ *</label>
          <div style={{ position: "relative" }}><input type="password" value={reg.confirmPw} onChange={e => setReg(f => ({ ...f, confirmPw: e.target.value }))} placeholder="à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦†à¦¬à¦¾à¦° à¦²à¦¿à¦–à§à¦¨" style={inputStyle({ paddingRight: 44, border: `1px solid ${reg.confirmPw === "" ? "rgba(255,255,255,0.1)" : reg.password === reg.confirmPw ? "rgba(16,185,129,0.5)" : "rgba(239,68,68,0.5)"}` })} />{reg.confirmPw && <div style={{ position: "absolute", right: 12, top: "50%", transform: "translateY(-50%)", fontSize: 14 }}>{reg.password === reg.confirmPw ? "âœ…" : "âŒ"}</div>}</div>
        </div>
        <div style={{ background: "rgba(99,102,241,0.08)", borderRadius: 10, padding: "11px 14px", border: "1px solid rgba(99,102,241,0.2)", marginBottom: 18, display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <span style={{ fontSize: 12, color: "#94A3B8" }}>à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ</span>
          <span style={{ fontSize: 18, fontWeight: 700, color: "#6366F1" }}>à§³{DEPOSIT_AMT.toLocaleString()}</span>
        </div>
        <Btn onClick={doRegister} color="green" disabled={!refValid}>âœ… à¦°à§‡à¦œà¦¿à¦¸à§à¦Ÿà§à¦°à§‡à¦¶à¦¨ à¦¸à¦®à§à¦ªà¦¨à§à¦¨ à¦•à¦°à§à¦¨</Btn>
      </div>
      <div style={{ textAlign: "center", marginTop: 12 }}>
        <span style={{ fontSize: 12, color: "#475569" }}>à¦‡à¦¤à¦¿à¦®à¦§à§à¦¯à§‡ à¦¸à¦¦à¦¸à§à¦¯? </span>
        <button onClick={() => { setScreen("login"); setMsg(""); }} style={{ background: "none", border: "none", color: "#6366F1", fontSize: 12, fontWeight: 700, cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif" }}>à¦²à¦—à¦‡à¦¨ à¦•à¦°à§à¦¨</button>
      </div>
    </div>
  );

  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  // ADMIN PANEL
  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  if (screen === "admin") {
    const pendingTx = transactions.filter(t => t.type === "deposit" && t.status === "pending");
    const allTx = transactions.filter(t => t.type === "deposit");
    const adminNode = all.find(n => n.id === 1);
    const adminTabs = [
      { id: "users", icon: "ðŸ‘¥", label: "à¦¸à¦¦à¦¸à§à¦¯" },
      { id: "deposits", icon: "ðŸ’³", label: "à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ" },
      { id: "agents", icon: "ðŸ“±", label: "à¦à¦œà§‡à¦¨à§à¦Ÿ" },
      { id: "settings", icon: "âš™ï¸", label: "à¦¸à§‡à¦Ÿà¦¿à¦‚à¦¸" },
    ];
    return wrap(
      <div style={{ minHeight: "100vh", display: "flex", flexDirection: "column" }}>
        {/* Admin Header */}
        <div style={{ padding: "14px 16px 10px", background: "rgba(8,8,18,0.95)", borderBottom: "1px solid rgba(255,255,255,0.06)", backdropFilter: "blur(20px)", position: "sticky", top: 0, zIndex: 10 }}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 10 }}>
            <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
              <div style={{ width: 34, height: 34, borderRadius: 10, background: "linear-gradient(135deg,#F59E0B,#D97706)", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 16 }}>ðŸ‘‘</div>
              <div><div style={{ fontSize: 14, fontWeight: 700, color: "#F59E0B" }}>Admin Panel</div><div style={{ fontSize: 10, color: "#475569" }}>à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸: à§³{(adminNode?.balance || 0).toLocaleString()}</div></div>
            </div>
            <div style={{ display: "flex", gap: 7 }}>
              {pendingTx.length > 0 && <div style={{ background: "rgba(239,68,68,0.2)", border: "1px solid rgba(239,68,68,0.3)", borderRadius: 8, padding: "4px 10px", fontSize: 11, color: "#F87171", fontWeight: 700 }}>â³ {pendingTx.length}</div>}
              <button onClick={() => { setUser(null); setScreen("login"); }} style={{ background: "rgba(239,68,68,0.1)", border: "1px solid rgba(239,68,68,0.2)", borderRadius: 8, color: "#F87171", padding: "6px 10px", fontSize: 11, cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif" }}>à¦²à¦—à¦†à¦‰à¦Ÿ</button>
            </div>
          </div>
          <div style={{ display: "flex", gap: 3 }}>
            {adminTabs.map(t => <button key={t.id} onClick={() => setAdminTab(t.id)} style={{ flex: 1, padding: "7px 2px", borderRadius: 8, border: "none", cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif", fontSize: 10, fontWeight: 600, background: adminTab === t.id ? "linear-gradient(135deg,#F59E0B,#D97706)" : "rgba(255,255,255,0.04)", color: adminTab === t.id ? "#fff" : "#475569", transition: "all 0.2s" }}>{t.icon} {t.label}</button>)}
          </div>
        </div>

        <div style={{ flex: 1, padding: "14px 15px 80px", overflowY: "auto" }}>
          <Flash m={adminMsg} />

          {/* â”€â”€ à¦¸à¦¦à¦¸à§à¦¯ â”€â”€ */}
          {adminTab === "users" && (
            <div>
              {adminEdit ? (
                <div>
                  <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 18 }}>
                    <button onClick={() => setAdminEdit(null)} style={{ background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.1)", color: "#94A3B8", borderRadius: 8, width: 32, height: 32, cursor: "pointer", fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center" }}>â†</button>
                    <div style={{ fontSize: 15, fontWeight: 700, color: "#E2E8F0" }}>{adminEdit.name} à¦¸à¦®à§à¦ªà¦¾à¦¦à¦¨à¦¾</div>
                  </div>

                  {/* Avatar edit */}
                  <div style={{ display: "flex", justifyContent: "center", marginBottom: 18 }}>
                    <Avatar node={adminEdit} size={72} editable onUpload={url => setAdminEdit(f => ({ ...f, avatar: url }))} />
                  </div>

                  <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 16, padding: "18px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 14 }}>
                    <SectionTitle icon="ðŸ‘¤" title="à¦¬à§à¦¯à¦•à§à¦¤à¦¿à¦—à¦¤ à¦¤à¦¥à§à¦¯" />
                    <TxtInp label="à¦¨à¦¾à¦®" value={adminEdit.name} onChange={v => setAdminEdit(f => ({ ...f, name: v }))} placeholder="à¦¨à¦¾à¦®" />
                    <TxtInp label="à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦°" value={adminEdit.phone} onChange={v => setAdminEdit(f => ({ ...f, phone: v }))} placeholder="01XXXXXXXXX" type="tel" />
                    <TxtInp label="NID à¦¨à¦®à§à¦¬à¦°" value={adminEdit.nid} onChange={v => setAdminEdit(f => ({ ...f, nid: v }))} placeholder="NID à¦¨à¦®à§à¦¬à¦°" />
                    <TxtInp label="à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡" value={adminEdit.referralCode} onChange={v => setAdminEdit(f => ({ ...f, referralCode: v }))} placeholder="à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡" />
                  </div>

                  <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 16, padding: "18px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 14 }}>
                    <SectionTitle icon="ðŸ’°" title="à¦†à¦°à§à¦¥à¦¿à¦• à¦¤à¦¥à§à¦¯" />
                    <TxtInp label="à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸ (à§³)" value={String(adminEdit.balance || 0)} onChange={v => setAdminEdit(f => ({ ...f, balance: parseFloat(v) || 0 }))} type="number" />
                    <TxtInp label="à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ (à§³)" value={String(adminEdit.deposit || 0)} onChange={v => setAdminEdit(f => ({ ...f, deposit: parseFloat(v) || 0 }))} type="number" />
                  </div>

                  <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 16, padding: "18px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 14 }}>
                    <SectionTitle icon="ðŸ”’" title="à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" />
                    <div style={{ marginBottom: 10 }}>
                      <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 5 }}>à¦¬à¦°à§à¦¤à¦®à¦¾à¦¨ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ (à¦¦à§ƒà¦¶à§à¦¯à¦®à¦¾à¦¨)</label>
                      <div style={{ background: "rgba(245,158,11,0.08)", border: "1px solid rgba(245,158,11,0.2)", borderRadius: 9, padding: "10px 14px", fontSize: 14, color: "#FCD34D", fontWeight: 700, letterSpacing: 2 }}>{adminEdit.password}</div>
                    </div>
                    <PwInp label="à¦¨à¦¤à§à¦¨ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ (à¦ªà¦°à¦¿à¦¬à¦°à§à¦¤à¦¨ à¦•à¦°à¦¤à§‡)" value={adminEdit.newPassword || ""} onChange={v => setAdminEdit(f => ({ ...f, newPassword: v }))} placeholder="à¦¨à¦¤à§à¦¨ à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡" />
                    {adminEdit.newPassword && <Btn small color="amber" onClick={() => setAdminEdit(f => ({ ...f, password: f.newPassword, newPassword: "" }))}>à¦ªà¦¾à¦¸à¦“à¦¯à¦¼à¦¾à¦°à§à¦¡ à¦ªà§à¦°à¦¯à¦¼à§‹à¦— à¦•à¦°à§à¦¨</Btn>}
                  </div>

                  <Btn onClick={doSaveUser} color="green">âœ… à¦ªà¦°à¦¿à¦¬à¦°à§à¦¤à¦¨ à¦¸à¦‚à¦°à¦•à§à¦·à¦£ à¦•à¦°à§à¦¨</Btn>
                </div>
              ) : (
                <div>
                  <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 8, marginBottom: 14 }}>
                    {[{ label: "à¦®à§‹à¦Ÿ à¦¸à¦¦à¦¸à§à¦¯", value: members.length, color: "#6366F1" }, { label: "à¦®à§‹à¦Ÿ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ", value: `à§³${(members.reduce((s, m) => s + (m.deposit || 0), 0) / 1000).toFixed(0)}k`, color: "#10B981" }].map(s => (
                      <div key={s.label} style={{ background: "rgba(255,255,255,0.03)", borderRadius: 12, padding: "14px", textAlign: "center", border: "1px solid rgba(255,255,255,0.05)" }}>
                        <div style={{ color: s.color, fontWeight: 700, fontSize: 22 }}>{s.value}</div>
                        <div style={{ color: "#475569", fontSize: 11, marginTop: 2 }}>{s.label}</div>
                      </div>
                    ))}
                  </div>
                  <div style={{ background: "rgba(255,255,255,0.02)", borderRadius: 13, overflow: "hidden", border: "1px solid rgba(255,255,255,0.05)" }}>
                    {members.map((m, i) => {
                      const col = LEVEL_COLORS[Math.min(m.level, 5)];
                      return (
                        <div key={m.id} style={{ display: "flex", alignItems: "center", padding: "11px 13px", borderBottom: i < members.length - 1 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                          <Avatar node={m} size={36} />
                          <div style={{ flex: 1, minWidth: 0, marginLeft: 10 }}>
                            <div style={{ fontSize: 12, fontWeight: 600, color: "#E2E8F0" }}>{m.name}</div>
                            <div style={{ fontSize: 10, color: "#374151" }}>ðŸ“± {m.phone} â€¢ <span style={{ color: col }}>Lv{m.level}</span></div>
                          </div>
                          <div style={{ textAlign: "right", marginRight: 8 }}>
                            <div style={{ color: "#10B981", fontSize: 11, fontWeight: 600 }}>à§³{(m.balance || 0).toLocaleString()}</div>
                            <div style={{ fontSize: 9, color: "#374151" }}>à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸</div>
                          </div>
                          <button onClick={() => setAdminEdit({ ...m })} style={{ background: "rgba(99,102,241,0.15)", border: "1px solid rgba(99,102,241,0.3)", color: "#A78BFA", borderRadius: 7, padding: "5px 10px", cursor: "pointer", fontSize: 11, fontFamily: "'Hind Siliguri',sans-serif" }}>à¦¸à¦®à§à¦ªà¦¾à¦¦à¦¨à¦¾</button>
                        </div>
                      );
                    })}
                  </div>
                </div>
              )}
            </div>
          )}

          {/* â”€â”€ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ à¦­à§‡à¦°à¦¿à¦«à¦¿à¦•à§‡à¦¶à¦¨ â”€â”€ */}
          {adminTab === "deposits" && (
            <div>
              {pendingTx.length > 0 && (
                <div style={{ marginBottom: 16 }}>
                  <div style={{ fontSize: 13, fontWeight: 700, color: "#F87171", marginBottom: 10 }}>â³ à¦…à¦ªà§‡à¦•à§à¦·à¦®à¦¾à¦£ à¦­à§‡à¦°à¦¿à¦«à¦¿à¦•à§‡à¦¶à¦¨ ({pendingTx.length}à¦Ÿà¦¿)</div>
                  {pendingTx.map(tx => (
                    <div key={tx.id} style={{ background: "rgba(239,68,68,0.06)", borderRadius: 14, padding: "14px 15px", marginBottom: 10, border: "1px solid rgba(239,68,68,0.15)" }}>
                      <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
                        <div style={{ fontSize: 13, fontWeight: 700, color: "#E2E8F0" }}>{tx.memberName}</div>
                        <div style={{ fontSize: 14, fontWeight: 700, color: "#10B981" }}>à§³{tx.amount.toLocaleString()}</div>
                      </div>
                      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 6, marginBottom: 10, fontSize: 11 }}>
                        <div><span style={{ color: "#475569" }}>à¦ªà¦¦à§à¦§à¦¤à¦¿: </span><span style={{ color: "#FCD34D" }}>{tx.method.toUpperCase()}</span></div>
                        <div><span style={{ color: "#475569" }}>à¦¤à¦¾à¦°à¦¿à¦–: </span><span style={{ color: "#CBD5E1" }}>{tx.date}</span></div>
                        <div><span style={{ color: "#475569" }}>TX ID: </span><span style={{ color: "#A78BFA", fontWeight: 700 }}>{tx.txId}</span></div>
                        <div><span style={{ color: "#475569" }}>à¦®à§‹à¦¬à¦¾à¦‡à¦²: </span><span style={{ color: "#CBD5E1" }}>{tx.senderPhone}</span></div>
                      </div>
                      <button onClick={() => doVerifyDeposit(tx.id)} style={{ width: "100%", padding: "10px", borderRadius: 9, border: "none", background: "linear-gradient(135deg,#10B981,#059669)", color: "#fff", fontSize: 13, fontWeight: 700, fontFamily: "'Hind Siliguri',sans-serif", cursor: "pointer" }}>âœ… à¦­à§‡à¦°à¦¿à¦«à¦¾à¦‡ à¦•à¦°à§à¦¨ â€” à¦•à¦®à¦¿à¦¶à¦¨ à¦¬à¦¿à¦¤à¦°à¦£ à¦•à¦°à§à¦¨</button>
                    </div>
                  ))}
                </div>
              )}
              <div style={{ fontSize: 12, fontWeight: 700, color: "#94A3B8", marginBottom: 10 }}>à¦¸à¦•à¦² à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ ({allTx.length}à¦Ÿà¦¿)</div>
              {allTx.length === 0 ? (
                <div style={{ textAlign: "center", color: "#374151", fontSize: 12, padding: "30px 0" }}>à¦•à§‹à¦¨à§‹ à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦¨à§‡à¦‡</div>
              ) : allTx.slice().reverse().map((tx, i) => (
                <div key={tx.id} style={{ background: "rgba(255,255,255,0.02)", borderRadius: 12, padding: "12px 14px", marginBottom: 8, border: `1px solid ${tx.status === "confirmed" ? "rgba(16,185,129,0.15)" : "rgba(245,158,11,0.15)"}` }}>
                  <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 4 }}>
                    <div style={{ fontSize: 12, fontWeight: 600, color: "#E2E8F0" }}>{tx.memberName}</div>
                    <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
                      <span style={{ fontSize: 13, fontWeight: 700, color: "#10B981" }}>à§³{tx.amount.toLocaleString()}</span>
                      <span style={{ fontSize: 10, padding: "2px 8px", borderRadius: 20, background: tx.status === "confirmed" ? "rgba(16,185,129,0.15)" : "rgba(245,158,11,0.15)", color: tx.status === "confirmed" ? "#34D399" : "#FCD34D" }}>{tx.status === "confirmed" ? "âœ… à¦¨à¦¿à¦¶à§à¦šà¦¿à¦¤" : "â³ à¦…à¦ªà§‡à¦•à§à¦·à¦®à¦¾à¦£"}</span>
                    </div>
                  </div>
                  <div style={{ fontSize: 10, color: "#475569" }}>TX: {tx.txId} â€¢ {tx.method.toUpperCase()} â€¢ {tx.date}</div>
                </div>
              ))}
            </div>
          )}

          {/* â”€â”€ à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¨à¦®à§à¦¬à¦° â”€â”€ */}
          {adminTab === "agents" && (
            <div>
              <div style={{ fontSize: 12, color: "#64748B", marginBottom: 14 }}>à¦•à¦¾à¦¸à§à¦Ÿà¦®à¦¾à¦°à¦°à¦¾ à¦à¦‡ à¦¨à¦®à§à¦¬à¦°à¦—à§à¦²à§‹à¦¤à§‡ à¦ªà§‡à¦®à§‡à¦¨à§à¦Ÿ à¦ªà¦¾à¦ à¦¾à¦¬à§‡</div>
              {Object.entries(agents).map(([key, ag]) => (
                <div key={key} style={{ background: "rgba(255,255,255,0.03)", borderRadius: 14, padding: "16px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 12 }}>
                  <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 12 }}>
                    <div style={{ fontSize: 20 }}>{key === "bkash" ? "ðŸ’—" : key === "nagad" ? "ðŸŸ " : "ðŸš€"}</div>
                    <div style={{ fontSize: 14, fontWeight: 700, color: "#E2E8F0" }}>{ag.name}</div>
                  </div>
                  <TxtInp label="à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¨à¦®à§à¦¬à¦°" value={ag.number} onChange={v => setAgents(prev => ({ ...prev, [key]: { ...prev[key], number: v } }))} placeholder="01XXXXXXXXX" type="tel" />
                  <TxtInp label="à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¨à¦¾à¦®" value={ag.name} onChange={v => setAgents(prev => ({ ...prev, [key]: { ...prev[key], name: v } }))} placeholder="à¦¨à¦¾à¦®" />
                </div>
              ))}
              <Flash m={adminMsg} />
              <Btn onClick={() => aFlash("âœ… à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¤à¦¥à§à¦¯ à¦¸à¦‚à¦°à¦•à§à¦·à¦¿à¦¤ à¦¹à¦¯à¦¼à§‡à¦›à§‡!")} color="green">ðŸ’¾ à¦¸à¦‚à¦°à¦•à§à¦·à¦£ à¦•à¦°à§à¦¨</Btn>
            </div>
          )}

          {/* â”€â”€ à¦¸à§‡à¦Ÿà¦¿à¦‚à¦¸ â”€â”€ */}
          {adminTab === "settings" && (
            <div>
              <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 14, padding: "16px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 14 }}>
                <SectionTitle icon="â›“ï¸" title="à¦šà§‡à¦‡à¦¨ à¦•à¦®à¦¿à¦¶à¦¨ à¦¹à¦¾à¦° (à§³à§«,à§¦à§¦à§¦ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ)" />
                {CHAIN_LABELS.map((label, i) => (
                  <div key={i} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "8px 0", borderBottom: i < 3 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                    <span style={{ fontSize: 12, color: "#94A3B8" }}>{label}</span>
                    <span style={{ fontSize: 13, fontWeight: 700, color: ["#10B981", "#3B82F6", "#EC4899", "#8B5CF6"][i] }}>à§³{(DEPOSIT_AMT * CHAIN_RATES[i]).toLocaleString()}</span>
                  </div>
                ))}
              </div>
              <div style={{ background: "rgba(245,158,11,0.07)", borderRadius: 14, padding: "16px", border: "1px solid rgba(245,158,11,0.15)" }}>
                <SectionTitle icon="ðŸ“Š" title="à¦¸à¦¿à¦¸à§à¦Ÿà§‡à¦® à¦ªà¦°à¦¿à¦¸à¦‚à¦–à§à¦¯à¦¾à¦¨" />
                {[
                  ["à¦®à§‹à¦Ÿ à¦¸à¦¦à¦¸à§à¦¯", members.length],
                  ["à¦®à§‹à¦Ÿ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ", `à§³${members.reduce((s, m) => s + (m.deposit || 0), 0).toLocaleString()}`],
                  ["à¦¨à¦¿à¦¶à§à¦šà¦¿à¦¤ TX", transactions.filter(t => t.status === "confirmed" && t.type === "deposit").length],
                  ["à¦…à¦ªà§‡à¦•à§à¦·à¦®à¦¾à¦£ TX", pendingTx.length],
                  ["à¦…à§à¦¯à¦¾à¦¡à¦®à¦¿à¦¨ à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸", `à§³${(adminNode?.balance || 0).toLocaleString()}`],
                ].map(([l, v]) => (
                  <div key={l} style={{ display: "flex", justifyContent: "space-between", padding: "7px 0", borderBottom: "1px solid rgba(255,255,255,0.04)" }}>
                    <span style={{ fontSize: 12, color: "#94A3B8" }}>{l}</span>
                    <span style={{ fontSize: 12, color: "#FCD34D", fontWeight: 600 }}>{v}</span>
                  </div>
                ))}
              </div>
            </div>
          )}
        </div>
      </div>
    );
  }

  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  // USER APP
  // â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
  const userNode = all.find(n => n.id === user?.id) || user;
  const userComm = userNode ? calcComm(userNode, all) : null;
  const userTx = transactions.filter(t => t.type === "deposit" && t.memberId === user?.id);
  const totalDep = members.reduce((s, m) => s + m.deposit, 0);

  const appTabs = [
    { id: "profile", icon: "ðŸ‘¤", label: "à¦ªà§à¦°à§‹à¦«à¦¾à¦‡à¦²" },
    { id: "deposit", icon: "ðŸ’³", label: "à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ" },
    { id: "commission", icon: "ðŸ’°", label: "à¦•à¦®à¦¿à¦¶à¦¨" },
    { id: "history", icon: "ðŸ“‹", label: "à¦¹à¦¿à¦¸à§à¦Ÿà§à¦°à¦¿" },
    { id: "tree", icon: "ðŸŒ³", label: "à¦Ÿà§à¦°à¦¿" },
  ];

  return wrap(
    <div style={{ minHeight: "100vh", display: "flex", flexDirection: "column" }}>
      {/* Header */}
      <div style={{ padding: "13px 15px 9px", background: "rgba(8,8,18,0.95)", borderBottom: "1px solid rgba(255,255,255,0.05)", backdropFilter: "blur(20px)", position: "sticky", top: 0, zIndex: 10 }}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 9 }}>
          <div style={{ display: "flex", alignItems: "center", gap: 9 }}>
            <Avatar node={userNode} size={34} editable onUpload={url => updateUser(user.id, n => ({ ...n, avatar: url }))} />
            <div>
              <div style={{ fontSize: 13, fontWeight: 700, color: "#E2E8F0" }}>{userNode.name}</div>
              <div style={{ fontSize: 10, color: "#374151" }}>{userNode.referralCode} â€¢ Lv{userNode.level}</div>
            </div>
          </div>
          <div style={{ display: "flex", gap: 7, alignItems: "center" }}>
            <div style={{ textAlign: "right" }}>
              <div style={{ fontSize: 13, fontWeight: 700, color: "#10B981" }}>à§³{(userNode.balance || 0).toLocaleString()}</div>
              <div style={{ fontSize: 9, color: "#374151" }}>à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸</div>
            </div>
            <button onClick={() => { setUser(null); setScreen("login"); }} style={{ background: "rgba(239,68,68,0.1)", border: "1px solid rgba(239,68,68,0.2)", borderRadius: 8, color: "#F87171", padding: "5px 9px", fontSize: 10, cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif" }}>à¦²à¦—à¦†à¦‰à¦Ÿ</button>
          </div>
        </div>
        <div style={{ display: "flex", gap: 3 }}>
          {appTabs.map(t => <button key={t.id} onClick={() => setTab(t.id)} style={{ flex: 1, padding: "6px 1px", borderRadius: 8, border: "none", cursor: "pointer", fontFamily: "'Hind Siliguri',sans-serif", fontSize: 9, fontWeight: 600, background: tab === t.id ? "linear-gradient(135deg,#6366F1,#8B5CF6)" : "rgba(255,255,255,0.04)", color: tab === t.id ? "#fff" : "#475569", transition: "all 0.2s" }}>{t.icon} {t.label}</button>)}
        </div>
      </div>

      <div style={{ flex: 1, padding: "13px 14px 80px", overflowY: "auto" }}>
        <Flash m={msg} />

        {/* â”€â”€ à¦ªà§à¦°à§‹à¦«à¦¾à¦‡à¦² â”€â”€ */}
        {tab === "profile" && (
          <div>
            <div style={{ background: "linear-gradient(135deg,#1E1B4B,#312E81,#1E1B4B)", borderRadius: 18, padding: "20px", marginBottom: 13, border: "1px solid rgba(99,102,241,0.3)", position: "relative", overflow: "hidden" }}>
              <div style={{ position: "absolute", top: -25, right: -25, width: 100, height: 100, background: "rgba(99,102,241,0.15)", borderRadius: "50%" }} />
              <div style={{ display: "flex", alignItems: "center", gap: 14 }}>
                <Avatar node={userNode} size={64} editable onUpload={url => { updateUser(user.id, n => ({ ...n, avatar: url })); flash("âœ… à¦›à¦¬à¦¿ à¦†à¦ªà¦²à§‹à¦¡ à¦¹à¦¯à¦¼à§‡à¦›à§‡!"); }} />
                <div>
                  <div style={{ fontSize: 16, fontWeight: 700, color: "#fff" }}>{userNode.name}</div>
                  <div style={{ fontSize: 10, color: "rgba(255,255,255,0.45)", marginBottom: 6 }}>#{userNode.id} â€¢ à¦²à§‡à¦­à§‡à¦² {userNode.level} ({LEVEL_LABELS[userNode.level]})</div>
                  <div style={{ display: "inline-flex", alignItems: "center", gap: 4, background: "rgba(245,158,11,0.2)", border: "1px solid rgba(245,158,11,0.3)", borderRadius: 20, padding: "3px 10px" }}>
                    <span style={{ color: "#FBB924", fontSize: 11, fontWeight: 700 }}>ðŸ… {LEVEL_LABELS[userNode.level]} à¦°â€à§à¦¯à¦¾à¦‚à¦•</span>
                  </div>
                </div>
              </div>
            </div>

            {/* à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡ */}
            <div style={{ background: "linear-gradient(135deg,#064E3B,#065F46)", borderRadius: 13, padding: "13px 15px", marginBottom: 13, border: "1px solid rgba(52,211,153,0.2)" }}>
              <div style={{ fontSize: 11, color: "#6EE7B7", marginBottom: 6, fontWeight: 600 }}>ðŸŽ à¦†à¦ªà¦¨à¦¾à¦° à¦°à§‡à¦«à¦¾à¦°à§‡à¦² à¦•à§‹à¦¡</div>
              <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between" }}>
                <span style={{ color: "#fff", fontSize: 20, fontWeight: 700, letterSpacing: 3 }}>{userNode.referralCode}</span>
                <button onClick={() => navigator.clipboard?.writeText(userNode.referralCode).then(() => flash("âœ… à¦•à§‹à¦¡ à¦•à¦ªà¦¿ à¦¹à¦¯à¦¼à§‡à¦›à§‡!"))} style={{ background: "rgba(52,211,153,0.2)", border: "1px solid rgba(52,211,153,0.35)", color: "#34D399", borderRadius: 8, padding: "6px 12px", cursor: "pointer", fontSize: 11, fontFamily: "'Hind Siliguri',sans-serif", fontWeight: 600 }}>ðŸ“‹ à¦•à¦ªà¦¿</button>
              </div>
              <div style={{ fontSize: 10, color: "rgba(52,211,153,0.6)", marginTop: 5 }}>à¦à¦‡ à¦•à§‹à¦¡ à¦¶à§‡à¦¯à¦¼à¦¾à¦° à¦•à¦°à§à¦¨ â€” à¦¨à¦¤à§à¦¨ à¦¸à¦¦à¦¸à§à¦¯ à¦à¦‡ à¦•à§‹à¦¡ à¦¬à§à¦¯à¦¬à¦¹à¦¾à¦° à¦•à¦°à¦²à§‡ à¦†à¦ªà¦¨à¦¾à¦° à¦¨à¦¿à¦šà§‡ à¦¯à§‹à¦— à¦¹à¦¬à§‡</div>
            </div>

            {/* Stats */}
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 9, marginBottom: 13 }}>
              {[
                { label: "à¦•à¦®à¦¿à¦¶à¦¨ à¦†à¦¯à¦¼", value: `à§³${(userComm?.total || 0).toLocaleString()}`, icon: "ðŸ’°", color: "#10B981" },
                { label: "à¦¬à§à¦¯à¦¾à¦²à§‡à¦¨à§à¦¸", value: `à§³${(userNode.balance || 0).toLocaleString()}`, icon: "ðŸ’³", color: "#6366F1" },
                { label: "à¦°à§‡à¦«à¦¾à¦°à§‡à¦²", value: userNode.children.length, icon: "ðŸ‘¥", color: "#F472B6" },
                { label: "à¦Ÿà¦¿à¦® à¦¸à¦¾à¦‡à¦œ", value: flatTree(userNode).length - 1, icon: "ðŸŒ", color: "#FBBF24" },
              ].map(s => (
                <div key={s.label} style={{ background: "rgba(255,255,255,0.03)", borderRadius: 13, padding: "14px", border: "1px solid rgba(255,255,255,0.05)" }}>
                  <div style={{ fontSize: 18, marginBottom: 5 }}>{s.icon}</div>
                  <div style={{ color: s.color, fontWeight: 700, fontSize: 17 }}>{s.value}</div>
                  <div style={{ color: "#374151", fontSize: 10 }}>{s.label}</div>
                </div>
              ))}
            </div>

            {/* Info */}
            <div style={{ background: "rgba(255,255,255,0.02)", borderRadius: 13, overflow: "hidden", border: "1px solid rgba(255,255,255,0.05)" }}>
              {[
                { icon: "ðŸ“±", label: "à¦®à§‹à¦¬à¦¾à¦‡à¦²", value: userNode.phone || "â€”" },
                { icon: "ðŸªª", label: "NID", value: userNode.nid ? userNode.nid.slice(0, 4) + "â—â—â—" + userNode.nid.slice(-2) : "â€”" },
                { icon: "ðŸ†”", label: "à¦¸à¦¦à¦¸à§à¦¯ à¦†à¦‡à¦¡à¦¿", value: `#${userNode.id}` },
                { icon: "ðŸ“Š", label: "à¦²à§‡à¦­à§‡à¦²", value: `${userNode.level} (${LEVEL_LABELS[userNode.level]})` },
              ].map((row, i, arr) => (
                <div key={row.label} style={{ display: "flex", alignItems: "center", padding: "11px 14px", borderBottom: i < arr.length - 1 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                  <span style={{ fontSize: 15, marginRight: 10 }}>{row.icon}</span>
                  <span style={{ flex: 1, fontSize: 12, color: "#64748B" }}>{row.label}</span>
                  <span style={{ fontSize: 12, color: "#CBD5E1", fontWeight: 500 }}>{row.value}</span>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* â”€â”€ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ â”€â”€ */}
        {tab === "deposit" && (
          <div>
            {/* Payment methods */}
            <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 16, padding: "16px", border: "1px solid rgba(255,255,255,0.07)", marginBottom: 14 }}>
              <SectionTitle icon="ðŸ“±" title="à¦ªà§‡à¦®à§‡à¦¨à§à¦Ÿ à¦à¦œà§‡à¦¨à§à¦Ÿ à¦¨à¦®à§à¦¬à¦°" />
              <AgentSelector agents={agents} onCopy={(num) => navigator.clipboard?.writeText(num).then(() => flash("âœ… à¦¨à¦®à§à¦¬à¦° à¦•à¦ªà¦¿ à¦¹à¦¯à¦¼à§‡à¦›à§‡!"))} />
            </div>

            {/* Deposit form */}
            <div style={{ background: "rgba(255,255,255,0.03)", borderRadius: 16, padding: "16px", border: "1px solid rgba(255,255,255,0.07)" }}>
              <SectionTitle icon="ðŸ’¸" title="à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ à¦¸à¦¾à¦¬à¦®à¦¿à¦Ÿ à¦•à¦°à§à¦¨" />
              <div style={{ marginBottom: 13 }}>
                <label style={{ fontSize: 12, color: "#94A3B8", display: "block", marginBottom: 8 }}>à¦ªà§‡à¦®à§‡à¦¨à§à¦Ÿ à¦ªà¦¦à§à¦§à¦¤à¦¿</label>
                <div style={{ display: "flex", gap: 8 }}>
                  {Object.entries(agents).map(([key, ag]) => (
                    <button key={key} onClick={() => setDepForm(f => ({ ...f, method: key }))} style={{ flex: 1, padding: "9px 4px", borderRadius: 9, border: `2px solid ${depForm.method === key ? "#6366F1" : "rgba(255,255,255,0.08)"}`, background: depForm.method === key ? "rgba(99,102,241,0.15)" : "rgba(255,255,255,0.03)", color: depForm.method === key ? "#A78BFA" : "#64748B", cursor: "pointer", fontSize: 11, fontFamily: "'Hind Siliguri',sans-serif", fontWeight: 700, transition: "all 0.2s" }}>
                      <div>{key === "bkash" ? "ðŸ’—" : key === "nagad" ? "ðŸŸ " : "ðŸš€"}</div>
                      <div>{ag.name}</div>
                    </button>
                  ))}
                </div>
              </div>
              <TxtInp label="à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦†à¦‡à¦¡à¦¿" value={depForm.txId} onChange={v => setDepForm(f => ({ ...f, txId: v }))} placeholder="à¦ªà§‡à¦®à§‡à¦¨à§à¦Ÿà§‡à¦° à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦†à¦‡à¦¡à¦¿" required />
              <TxtInp label="à¦†à¦ªà¦¨à¦¾à¦° à¦®à§‹à¦¬à¦¾à¦‡à¦² à¦¨à¦®à§à¦¬à¦° (à¦¯à§‡à¦Ÿà¦¾ à¦¥à§‡à¦•à§‡ à¦ªà¦¾à¦ à¦¿à¦¯à¦¼à§‡à¦›à§‡à¦¨)" value={depForm.phone} onChange={v => setDepForm(f => ({ ...f, phone: v }))} placeholder="01XXXXXXXXX" type="tel" required />
              <TxtInp label="à¦ªà¦°à¦¿à¦®à¦¾à¦£ (à§³)" value={String(depForm.amount)} onChange={v => setDepForm(f => ({ ...f, amount: parseFloat(v) || 0 }))} type="number" />
              <div style={{ background: "rgba(16,185,129,0.07)", borderRadius: 10, padding: "10px 13px", marginBottom: 14, border: "1px solid rgba(16,185,129,0.15)", fontSize: 11, color: "#6EE7B7" }}>
                â„¹ï¸ à¦¸à¦¾à¦¬à¦®à¦¿à¦Ÿà§‡à¦° à¦ªà¦° à¦…à§à¦¯à¦¾à¦¡à¦®à¦¿à¦¨ à¦­à§‡à¦°à¦¿à¦«à¦¾à¦‡ à¦•à¦°à¦²à§‡ à¦•à¦®à¦¿à¦¶à¦¨ à¦†à¦ªà¦¨à¦¾à¦° à¦‰à¦ªà¦°à§‡à¦° à¦¸à¦¦à¦¸à§à¦¯à¦¦à§‡à¦° à¦•à¦¾à¦›à§‡ à¦šà¦²à§‡ à¦¯à¦¾à¦¬à§‡
              </div>
              <Btn onClick={doSubmitDeposit} color="indigo">ðŸ“¤ à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ à¦¸à¦¾à¦¬à¦®à¦¿à¦Ÿ à¦•à¦°à§à¦¨</Btn>
            </div>
          </div>
        )}

        {/* â”€â”€ à¦•à¦®à¦¿à¦¶à¦¨ â”€â”€ */}
        {tab === "commission" && userComm && (
          <div>
            <div style={{ background: "linear-gradient(135deg,#0F2027,#203A43,#2C5364)", borderRadius: 17, padding: "18px", marginBottom: 13, border: "1px solid rgba(16,185,129,0.2)" }}>
              <div style={{ fontSize: 11, color: "#6EE7B7", marginBottom: 3 }}>à¦†à¦ªà¦¨à¦¾à¦° à¦®à§‹à¦Ÿ à¦•à¦®à¦¿à¦¶à¦¨ à¦†à¦¯à¦¼</div>
              <div style={{ fontSize: 30, fontWeight: 700, color: "#10B981" }}>à§³ {userComm.total.toLocaleString()}</div>
              <div style={{ fontSize: 10, color: "#475569", marginTop: 3 }}>{flatTree(userNode).length - 1} à¦¸à¦¦à¦¸à§à¦¯à§‡à¦° à¦¨à§‡à¦Ÿà¦“à¦¯à¦¼à¦¾à¦°à§à¦• à¦¥à§‡à¦•à§‡</div>
            </div>
            <div style={{ background: "rgba(255,255,255,0.02)", borderRadius: 14, overflow: "hidden", border: "1px solid rgba(255,255,255,0.05)", marginBottom: 13 }}>
              <div style={{ padding: "11px 14px", borderBottom: "1px solid rgba(255,255,255,0.05)" }}><span style={{ fontSize: 12, fontWeight: 700, color: "#A78BFA" }}>â›“ï¸ à¦šà§‡à¦‡à¦¨ à¦•à¦®à¦¿à¦¶à¦¨ à¦¬à¦¿à¦­à¦¾à¦œà¦¨</span></div>
              {userComm.lvls.map((row, i) => {
                const cols = ["#10B981", "#3B82F6", "#EC4899", "#8B5CF6"];
                return (
                  <div key={i} style={{ display: "flex", alignItems: "center", padding: "12px 14px", borderBottom: i < 3 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                    <div style={{ width: 26, height: 26, borderRadius: 8, background: cols[i] + "22", border: `1px solid ${cols[i]}44`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 11, fontWeight: 700, color: cols[i], marginRight: 10 }}>{i + 1}</div>
                    <div style={{ flex: 1 }}>
                      <div style={{ fontSize: 12, color: "#CBD5E1", fontWeight: 600 }}>{CHAIN_LABELS[i]}</div>
                      <div style={{ fontSize: 10, color: "#475569" }}>{row.count} à¦œà¦¨ Ã— à§³{(DEPOSIT_AMT * CHAIN_RATES[i]).toLocaleString()}</div>
                    </div>
                    <div style={{ color: cols[i], fontWeight: 700, fontSize: 13 }}>à§³{row.amt.toLocaleString()}</div>
                  </div>
                );
              })}
            </div>
            <div style={{ background: "rgba(245,158,11,0.07)", borderRadius: 13, padding: "14px", border: "1px solid rgba(245,158,11,0.15)" }}>
              <div style={{ fontSize: 12, color: "#FCD34D", fontWeight: 700, marginBottom: 9 }}>ðŸ“‹ à¦•à¦®à¦¿à¦¶à¦¨ à¦¨à¦¿à¦¯à¦¼à¦®à¦¾à¦¬à¦²à§€</div>
              {[["à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ", "à§³à§«,à§¦à§¦à§¦", "#F59E0B"], ["à§§à¦® à¦†à¦ªà¦²à¦¾à¦‡à¦¨", "à§¨à§«% = à§³à§§,à§¨à§«à§¦", "#10B981"], ["à§¨à¦¯à¦¼ à¦†à¦ªà¦²à¦¾à¦‡à¦¨", "à§¬à§¦% = à§³à§©,à§¦à§¦à§¦", "#3B82F6"], ["à§©à¦¯à¦¼ à¦†à¦ªà¦²à¦¾à¦‡à¦¨", "à§§.à§«% = à§³à§­à§«", "#EC4899"], ["à§ªà¦°à§à¦¥ à¦†à¦ªà¦²à¦¾à¦‡à¦¨", "à§§.à§«% = à§³à§­à§«", "#8B5CF6"], ["à§«à¦®+ à¦†à¦ªà¦²à¦¾à¦‡à¦¨", "à§¦%", "#475569"]].map(([l, v, c]) => (
                <div key={l} style={{ display: "flex", justifyContent: "space-between", padding: "5px 0", borderBottom: "1px solid rgba(255,255,255,0.04)" }}>
                  <span style={{ fontSize: 11, color: "#94A3B8" }}>{l}</span>
                  <span style={{ fontSize: 11, color: c, fontWeight: 600 }}>{v}</span>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* â”€â”€ à¦¹à¦¿à¦¸à§à¦Ÿà§à¦°à¦¿ â”€â”€ */}
        {tab === "history" && (
          <div>
            <div style={{ fontSize: 12, fontWeight: 700, color: "#94A3B8", marginBottom: 12 }}>à¦†à¦ªà¦¨à¦¾à¦° à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦¹à¦¿à¦¸à§à¦Ÿà§à¦°à¦¿</div>
            {userTx.length === 0 ? (
              <div style={{ textAlign: "center", color: "#374151", fontSize: 12, padding: "40px 0" }}>à¦•à§‹à¦¨à§‹ à¦Ÿà§à¦°à¦¾à¦¨à¦œà§‡à¦•à¦¶à¦¨ à¦¨à§‡à¦‡à¥¤<br />à¦¡à¦¿à¦ªà§‹à¦œà¦¿à¦Ÿ à¦Ÿà§à¦¯à¦¾à¦¬ à¦¥à§‡à¦•à§‡ à¦œà¦®à¦¾ à¦•à¦°à§à¦¨à¥¤</div>
            ) : userTx.slice().reverse().map((tx) => (
              <div key={tx.id} style={{ background: "rgba(255,255,255,0.02)", borderRadius: 13, padding: "13px 14px", marginBottom: 9, border: `1px solid ${tx.status === "confirmed" ? "rgba(16,185,129,0.15)" : "rgba(245,158,11,0.15)"}` }}>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 6 }}>
                  <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                    <span style={{ fontSize: 18 }}>{tx.method === "bkash" ? "ðŸ’—" : tx.method === "nagad" ? "ðŸŸ " : "ðŸš€"}</span>
                    <div>
                      <div style={{ fontSize: 12, fontWeight: 600, color: "#E2E8F0" }}>{agents[tx.method]?.name || tx.method}</div>
                      <div style={{ fontSize: 10, color: "#475569" }}>{tx.date}</div>
                    </div>
                  </div>
                  <div style={{ textAlign: "right" }}>
                    <div style={{ fontSize: 14, fontWeight: 700, color: "#10B981" }}>à§³{tx.amount.toLocaleString()}</div>
                    <div style={{ fontSize: 10, padding: "2px 8px", borderRadius: 20, background: tx.status === "confirmed" ? "rgba(16,185,129,0.15)" : "rgba(245,158,11,0.15)", color: tx.status === "confirmed" ? "#34D399" : "#FCD34D", marginTop: 3, display: "inline-block" }}>{tx.status === "confirmed" ? "âœ… à¦¨à¦¿à¦¶à§à¦šà¦¿à¦¤" : "â³ à¦…à¦ªà§‡à¦•à§à¦·à¦®à¦¾à¦£"}</div>
                  </div>
                </div>
                <div style={{ fontSize: 10, color: "#374151" }}>TX ID: <span style={{ color: "#A78BFA" }}>{tx.txId}</span> â€¢ à¦®à§‹à¦¬à¦¾à¦‡à¦²: {tx.senderPhone}</div>
              </div>
            ))}
          </div>
        )}

        {/* â”€â”€ à¦Ÿà§à¦°à¦¿ â”€â”€ */}
        {tab === "tree" && (
          <div>
            {selNode && (
              <div style={{ background: "rgba(99,102,241,0.08)", borderRadius: 12, padding: "10px 14px", marginBottom: 12, border: "1px solid rgba(99,102,241,0.2)" }}>
                <div style={{ display: "flex", justifyContent: "space-between" }}>
                  <div><div style={{ fontWeight: 700, color: "#A78BFA", fontSize: 13 }}>{selNode.name}</div><div style={{ fontSize: 10, color: "#374151" }}>Lv{selNode.level} â€¢ {selNode.referralCode}</div></div>
                  {selNode.level > 0 && <div style={{ textAlign: "right" }}><div style={{ color: "#10B981", fontWeight: 700, fontSize: 13 }}>à§³{calcComm(selNode, all).total.toLocaleString()}</div><div style={{ fontSize: 9, color: "#374151" }}>à¦•à¦®à¦¿à¦¶à¦¨</div></div>}
                </div>
              </div>
            )}
            <div style={{ background: "rgba(255,255,255,0.02)", borderRadius: 14, padding: "15px 8px", border: "1px solid rgba(255,255,255,0.05)", overflowX: "auto", minHeight: 220 }}>
              <div style={{ display: "flex", justifyContent: "center", minWidth: "max-content" }}>
                <TreeNode node={tree} onSelect={n => setSelNode(p => p?.id === n.id ? null : n)} selId={selNode?.id} />
              </div>
            </div>
          </div>
        )}
      </div>

      {/* Bottom Nav */}
      <div style={{ position: "fixed", bottom: 0, left: "50%", transform: "translateX(-50%)", width: "100%", maxWidth: 420, zIndex: 20, background: "rgba(8,8,18,0.97)", backdropFilter: "blur(20px)", borderTop: "1px solid rgba(255,255,255,0.05)", display: "flex", padding: "9px 0 16px" }}>
        {appTabs.map(t => (
          <button key={t.id} onClick={() => setTab(t.id)} style={{ flex: 1, display: "flex", flexDirection: "column", alignItems: "center", gap: 2, background: "none", border: "none", cursor: "pointer" }}>
            <span style={{ fontSize: 17 }}>{t.icon}</span>
            <span style={{ fontSize: 9, color: tab === t.id ? "#8B5CF6" : "#374151", fontFamily: "'Hind Siliguri',sans-serif", fontWeight: tab === t.id ? 700 : 400 }}>{t.label}</span>
            {tab === t.id && <div style={{ width: 3, height: 3, borderRadius: "50%", background: "#8B5CF6" }} />}
          </button>
        ))}
      </div>
    </div>
  );
}
