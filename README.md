import { useState } from "react";
const groups = [
{ id: "A", teams: [" Mexiko", " Südafrika", " Südkorea", " Tschechien"], note: "Me
{ id: "B", teams: [" Kanada", " Bosnien-Herzegowina", " Katar", " Schweiz"], note:
{ id: "C", teams: [" Brasilien", " Marokko", " Haiti", " Schottland"], note: "Bras
{ id: "D", teams: [" USA", " Paraguay", " Australien", " Türkei"], note: "Gastgebe
{ id: "E", teams: [" Deutschland", " Elfenbeinküste", " Ecuador", " Curaçao"], not
{ id: "F", teams: [" Niederlande", " Japan", " Tunesien", " Schweden"], note: "Tec
{ id: "G", teams: [" Belgien", " Ägypten", " Iran", " Neuseeland"], note: "Belgien
{ id: "H", teams: [" Spanien", " Uruguay", " Saudi-Arabien", " Kap Verde"], note:
{ id: "I", teams: [" Frankreich", " Senegal", " Norwegen", " Irak"], note: " Tod
{ id: "J", teams: [" Argentinien", " Österreich", " Algerien", " Jordanien"], note
{ id: "K", teams: [" Portugal", " Kolumbien", " Usbekistan", " DR Kongo"], note: "
{ id: "L", teams: [" England", " Kroatien", " Ghana", " Panama"], note: " Hammer
];
const rounds = [
{ name: "Gruppenphase", dates: "11. – 27. Juni 2026", icon: " " },
{ name: "Sechzehntelfinale", dates: "28. Juni – 3. Juli 2026", icon: "32" },
{ name: "Achtelfinale", dates: "4. – 7. Juli 2026", icon: "16" },
{ name: "Viertelfinale", dates: "9. – 11. Juli 2026", icon: "8" },
{ name: "Halbfinale", dates: "14. – 15. Juli 2026", icon: "4" },
{ name: "Spiel um Platz 3", dates: "18. Juli 2026", icon: " " },
{ name: "FINALE", dates: "19. Juli 2026", icon: " " },
];
const germanyGames = [
{ date: "14. Juni 2026", time: "19:00 Uhr", opponent: " { date: "20. Juni 2026", time: "22:00 Uhr", opponent: " { date: "25. Juni 2026", time: "22:00 Uhr", opponent: " Curaçao", tv: "ARD" },
Elfenbeinküste", tv: "ZDF" Ecuador", tv: "ARD/ZDF" },
},
];
const groupColors = {
A: "#e74c3c", B: "#e67e22", C: "#f1c40f", D: "#2ecc71",
E: "#3498db", F: "#9b59b6", G: "#1abc9c", H: "#e91e8c",
I: "#ff5722", J: "#607d8b", K: "#8bc34a", L: "#ff9800",
};
export default function WM2026() {
const [activeTab, setActiveTab] = useState("gruppen");
const [selectedGroup, setSelectedGroup] = useState(null);
return (
<div style={{
minHeight: "100vh",
background: "linear-gradient(135deg, #0a0a1a 0%, #0d1b2a 50%, #0a1628 100%)",
fontFamily: "'Georgia', 'Times New Roman', serif",
color: "#e8e0d0",
padding: "0",
}}>
{/* Header */}
<div style={{
background: "linear-gradient(180deg, #c8a400 0%, #a07800 100%)",
padding: "32px 24px 24px",
textAlign: "center",
position: "relative",
overflow: "hidden",
}}>
<div style={{
position: "absolute", inset: 0,
backgroundImage: "repeating-linear-gradient(45deg, transparent, transparent 10px, r
}} />
<div style={{ position: "relative" }}>
<div style={{ fontSize: "13px", letterSpacing: "4px", color: "#3a2000", marginBotto
FIFA Fußball-Weltmeisterschaft
</div>
<h1 style={{
fontSize: "clamp(36px, 8vw, 64px)",
fontWeight: "900",
color: "#1a0a00",
margin: "0 0 4px",
letterSpacing: "-1px",
lineHeight: 1,
}}>
WM 2026
</h1>
<div style={{ fontSize: "14px", color: "#3a2000", letterSpacing: "3px" }}>
USA · KANADA · MEXIKO
</div>
<div style={{ marginTop: "12px", fontSize: "13px", color: "#3a2000" }}>
48 Teams · 104 Spiele · 11. Juni – 19. Juli 2026
</div>
</div>
</div>
{/* Tab Navigation */}
<div style={{
display: "flex",
background: "#111827",
borderBottom: "1px solid #2a3a50",
}}>
{[
{ id: "gruppen", label: "Gruppen A–L" },
{ id: "spielplan", label: "Turnierphasen" },
{ id: "deutschland", label: " Deutschland" },
].map(tab => (
<button
key={tab.id}
onClick={() => setActiveTab(tab.id)}
style={{
flex: 1,
padding: "14px 8px",
background: activeTab === tab.id ? "#c8a400" : "transparent",
color: activeTab === tab.id ? "#1a0a00" : "#8a9bb0",
border: "none",
cursor: "pointer",
fontSize: "13px",
fontWeight: activeTab === tab.id ? "700" : "400",
letterSpacing: "1px",
transition: "all 0.2s",
fontFamily: "inherit",
}}
>
{tab.label}
</button>
))}
</div>
{/* Content */}
<div style={{ padding: "24px 16px", maxWidth: "800px", margin: "0 auto" }}>
{/* GRUPPEN TAB */}
{activeTab === "gruppen" && (
<div>
<p style={{ color: "#8a9bb0", fontSize: "13px", textAlign: "center", marginBottom
12 GRUPPEN · 4 TEAMS PRO GRUPPE · TOP 2 + BESTE 8 DRITTE WEITER
</p>
<div style={{ display: "grid", gap: "12px" }}>
{groups.map(group => (
<div
key={group.id}
onClick={() => setSelectedGroup(selectedGroup === group.id ? null : group.i
style={{
background: selectedGroup === group.id
? `linear-gradient(135deg, ${groupColors[group.id]}22, #1a2535)`
: "#111827",
border: `1px solid ${selectedGroup === group.id ? groupColors[group.id] :
borderRadius: "8px",
padding: "16px",
cursor: "pointer",
transition: "all 0.2s",
}}
>
<div style={{ display: "flex", alignItems: "center", gap: "16px" }}>
<div style={{
width: "44px", height: "44px",
background: groupColors[group.id],
borderRadius: "8px",
display: "flex", alignItems: "center", justifyContent: "center",
fontSize: "22px", fontWeight: "900",
color: "#fff",
flexShrink: 0,
}}>
{group.id}
</div>
<div style={{ flex: 1 }}>
<div style={{ display: "flex", flexWrap: "wrap", gap: "8px" }}>
{group.teams.map((team, i) => (
<span key={i} style={{
background: i === 0 ? `${groupColors[group.id]}33` : "#1e2d40",
border: i === 0 ? `1px solid ${groupColors[group.id]}66` : "1px s
borderRadius: "4px",
padding: "4px 10px",
fontSize: "13px",
color: i === 0 ? "#e8e0d0" : "#a0b0c0",
fontWeight: i === 0 ? "600" : "400",
}}>
{team}
</span>
))}
</div>
</div>
<div style={{ color: "#4a6a80", fontSize: "18px" }}>
{selectedGroup === group.id ? "▲" : "▼"}
</div>
</div>
{selectedGroup === group.id && (
<div style={{
marginTop: "12px",
paddingTop: "12px",
borderTop: `1px solid ${groupColors[group.id]}44`,
fontSize: "13px",
color: "#8a9bb0",
fontStyle: "italic",
}}>
{group.note}
</div>
)}
</div>
))}
</div>
</div>
)}
{/* SPIELPLAN TAB */}
{activeTab === "spielplan" && (
<div>
<p style={{ color: "#8a9bb0", fontSize: "13px", textAlign: "center", marginBottom
TURNIERPHASEN IM ÜBERBLICK
</p>
<div style={{ position: "relative" }}>
{/* Timeline line */}
<div style={{
position: "absolute",
left: "31px",
top: "0", bottom: "0",
width: "2px",
}} />
background: "linear-gradient(180deg, #c8a400, #8a5200, #c8a400)",
<div style={{ display: "flex", flexDirection: "column", gap: "16px" }}>
{rounds.map((round, i) => (
<div key={i} style={{ display: "flex", gap: "20px", alignItems: "flex-start
<div style={{
width: "44px", height: "44px",
background: round.name === "FINALE" ? "#c8a400" : "#1e2d40",
border: `2px solid ${round.name === "FINALE" ? "#c8a400" : "#2a3a50"}`,
borderRadius: "50%",
display: "flex", alignItems: "center", justifyContent: "center",
fontSize: round.icon.length > 2 ? "18px" : "11px",
fontWeight: "900",
color: round.name === "FINALE" ? "#1a0a00" : "#8a9bb0",
flexShrink: 0,
zIndex: 1,
}}>
{round.icon}
</div>
<div style={{
flex: 1,
background: round.name === "FINALE" ? "linear-gradient(135deg, #c8a4002
border: `1px solid ${round.name === "FINALE" ? "#c8a40066" : "#2a3a50"}
borderRadius: "8px",
padding: "14px 16px",
}}>
<div style={{
fontWeight: "700",
fontSize: round.name === "FINALE" ? "18px" : "15px",
color: round.name === "FINALE" ? "#c8a400" : "#e8e0d0",
letterSpacing: round.name === "FINALE" ? "2px" : "0",
}}>
{round.name}
</div>
<div style={{ fontSize: "13px", color: "#6a8a9a", marginTop: "4px" }}>
{round.dates}
</div>
{round.name === "FINALE" && (
<div style={{ fontSize: "12px", color: "#c8a400", marginTop: "6px" }}
MetLife Stadium, New York/New Jersey
</div>
)}
{round.name === "Gruppenphase" && (
<div style={{ fontSize: "12px", color: "#6a8a9a", marginTop: "6px" }}
72 Spiele · 12 Gruppen à 6 Begegnungen
</div>
)}
{round.name === "Sechzehntelfinale" && (
<div style={{ fontSize: "12px", color: "#6a8a9a", marginTop: "6px" }}
Neu 2026: 32 Teams · Gruppendritte vs. Gruppenerste
</div>
)}
</div>
</div>
))}
</div>
</div>
<div style={{
marginTop: "24px",
background: "#111827",
border: "1px solid #2a3a50",
borderRadius: "8px",
padding: "16px",
}}>
<div style={{ fontWeight: "700", marginBottom: "8px", color: "#c8a400" }}>Neuer
<div style={{ fontSize: "13px", color: "#8a9bb0", lineHeight: "1.8" }}>
• 48 Nationen in 12 Vierergruppen (A–L)<br />
• Top 2 jeder Gruppe + beste 8 Gruppendritt = 32 Teams weiter<br />
• Erstmals Sechzehntelfinale in der WM-Geschichte<br />
• Insgesamt 104 Spiele in 39 Tagen
</div>
</div>
</div>
)}
{/* DEUTSCHLAND TAB */}
{activeTab === "deutschland" && (
<div>
<div style={{
background: "linear-gradient(135deg, #3498db22, #1a2535)",
border: "1px solid #3498db66",
borderRadius: "8px",
padding: "20px",
marginBottom: "20px",
textAlign: "center",
}}>
<div style={{ fontSize: "40px", marginBottom: "8px" }}> </div>
<div style={{ fontSize: "22px", fontWeight: "700", color: "#e8e0d0" }}>Deutschl
<div style={{
display: "inline-block",
background: "#3498db",
borderRadius: "20px",
padding: "4px 16px",
fontSize: "13px",
fontWeight: "700",
color: "#fff",
marginTop: "8px",
letterSpacing: "2px",
}}>
GRUPPE E
</div>
<div style={{ marginTop: "8px", fontSize: "13px", color: "#8a9bb0" }}>
Trainer: Julian Nagelsmann · FIFA-Rang 9
</div>
</div>
<div style={{ fontWeight: "700", marginBottom: "12px", color: "#c8a400", letterSp
GRUPPENSPIELE
</div>
{germanyGames.map((game, i) => (
<div key={i} style={{
background: "#111827",
border: "1px solid #2a3a50",
borderRadius: "8px",
padding: "16px",
marginBottom: "10px",
display: "flex",
justifyContent: "space-between",
alignItems: "center",
}}>
<div>
<div style={{ fontSize: "14px", fontWeight: "600", color: "#e8e0d0", Deutschland vs. {game.opponent}
margin
</div>
<div style={{ fontSize: "12px", color: "#6a8a9a" }}>
{game.date} · {game.time}
</div>
</div>
<div style={{
background: "#1e2d40",
border: "1px solid #2a3a50",
borderRadius: "4px",
padding: "4px 10px",
fontSize: "12px",
color: "#c8a400",
fontWeight: "700",
}}>
{game.tv}
</div>
</div>
))}
<div style={{
background: "#111827",
border: "1px solid #2a3a50",
borderRadius: "8px",
padding: "16px",
marginTop: "16px",
}}>
<div style={{ fontWeight: "700", marginBottom: "12px", color: "#c8a400", GRUPPE E – ALLE TEAMS
</div>
{[" Deutschland (Favorit)", " Elfenbeinküste (Afrika-Cup-Sieger 2024)", "
<div key={i} style={{
display: "flex",
alignItems: "center",
gap: "12px",
padding: "10px 0",
borderBottom: i < 3 ? "1px solid #1e2d40" : "none",
}}>
letter
<div style={{
width: "24px", height: "24px",
background: i === 0 ? "#3498db" : "#1e2d40",
borderRadius: "50%",
display: "flex", alignItems: "center", justifyContent: "center",
fontSize: "12px", fontWeight: "700",
color: "#e8e0d0",
flexShrink: 0,
}}>
{i + 1}
</div>
</div>
<span style={{ fontSize: "14px", color: i === 0 ? "#e8e0d0" : "#8a9bb0" }}>
))}
</div>
<div style={{
marginTop: "16px",
background: "linear-gradient(135deg, #c8a40011, #1a2535)",
border: "1px solid #c8a40044",
borderRadius: "8px",
padding: "16px",
fontSize: "13px",
color: "#8a9bb0",
lineHeight: "1.8",
}}>
<span style={{ color: "#c8a400", fontWeight: "700" }}>Turnierpfad: </span>
Als Gruppensieger geht es im Sechzehntelfinale gegen einen Gruppendritten aus d
</div>
</div>
)}
</div>
{/* Footer */}
<div style={{ textAlign: "center", padding: "24px", color: "#3a4a5a", fontSize: "11px",
FIFA WM 2026 · USA · KANADA · MEXIKO · FINALE 19. JULI 2026
</div>
</div>
);
)
