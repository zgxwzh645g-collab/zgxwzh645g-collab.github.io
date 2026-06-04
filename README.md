cat > /mnt/user-data/outputs/index.html << 'HTMLEOF'
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WM 2026 Spielplan</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.2/babel.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: #0a0a1a; }
  </style>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    const { useState } = React;

    const groups = [
      { id: "A", teams: ["🇲🇽 Mexiko", "🇿🇦 Südafrika", "🇰🇷 Südkorea", "🇨🇿 Tschechien"], note: "Mexiko spielt alle Heimspiele im Aztekenstadion" },
      { id: "B", teams: ["🇨🇦 Kanada", "🇧🇦 Bosnien-Herzegowina", "🇶🇦 Katar", "🇨🇭 Schweiz"], note: "Gastgeber Kanada als Mitfavorit" },
      { id: "C", teams: ["🇧🇷 Brasilien", "🇲🇦 Marokko", "🇭🇹 Haiti", "🏴󠁧󠁢󠁳󠁣󠁴󠁿 Schottland"], note: "Brasilien vs. Marokko – der Kracher zum Auftakt" },
      { id: "D", teams: ["🇺🇸 USA", "🇵🇾 Paraguay", "🇦🇺 Australien", "🇹🇷 Türkei"], note: "Gastgeber USA unter Heimdruck" },
      { id: "E", teams: ["🇩🇪 Deutschland", "🇨🇮 Elfenbeinküste", "🇪🇨 Ecuador", "🇨🇼 Curaçao"], note: "🏆 DFB-Gruppe – Favorit Deutschland" },
      { id: "F", teams: ["🇳🇱 Niederlande", "🇯🇵 Japan", "🇹🇳 Tunesien", "🇸🇪 Schweden"], note: "Technisch hochklassiges Duell NL vs. Japan" },
      { id: "G", teams: ["🇧🇪 Belgien", "🇪🇬 Ägypten", "🇮🇷 Iran", "🇳🇿 Neuseeland"], note: "Belgien als klarer Gruppensieger erwartet" },
      { id: "H", teams: ["🇪🇸 Spanien", "🇺🇾 Uruguay", "🇸🇦 Saudi-Arabien", "🇨🇻 Kap Verde"], note: "Europameister Spanien trifft auf Uruguay" },
      { id: "I", teams: ["🇫🇷 Frankreich", "🇸🇳 Senegal", "🇳🇴 Norwegen", "🇮🇶 Irak"], note: "💀 Todesgruppe – Weltranglisten-Erste Frankreich" },
      { id: "J", teams: ["🇦🇷 Argentinien", "🇦🇹 Österreich", "🇩🇿 Algerien", "🇯🇴 Jordanien"], note: "Titelverteidiger Argentinien als Topfavorit" },
      { id: "K", teams: ["🇵🇹 Portugal", "🇨🇴 Kolumbien", "🇺🇿 Usbekistan", "🇨🇩 DR Kongo"], note: "Ronaldos letzte WM-Chance?" },
      { id: "L", teams: ["🏴󠁧󠁢󠁥󠁮󠁧󠁿 England", "🇭🇷 Kroatien", "🇬🇭 Ghana", "🇵🇦 Panama"], note: "💪 Hammergruppe – stärkste aller 12 Gruppen" },
    ];

    const rounds = [
      { name: "Gruppenphase", dates: "11. – 27. Juni 2026", icon: "⚽", extra: "72 Spiele · 12 Gruppen à 6 Begegnungen" },
      { name: "Sechzehntelfinale", dates: "28. Juni – 3. Juli 2026", icon: "32", extra: "Neu 2026: 32 Teams · Gruppendritte vs. Gruppenerste" },
      { name: "Achtelfinale", dates: "4. – 7. Juli 2026", icon: "16", extra: "" },
      { name: "Viertelfinale", dates: "9. – 11. Juli 2026", icon: "8", extra: "" },
      { name: "Halbfinale", dates: "14. – 15. Juli 2026", icon: "4", extra: "" },
      { name: "Spiel um Platz 3", dates: "18. Juli 2026", icon: "🥉", extra: "" },
      { name: "FINALE", dates: "19. Juli 2026", icon: "🏆", extra: "🏟️ MetLife Stadium, New York/New Jersey" },
    ];

    const germanyGames = [
      { date: "14. Juni 2026", time: "19:00 Uhr", opponent: "🇨🇼 Curaçao", tv: "ARD" },
      { date: "20. Juni 2026", time: "22:00 Uhr", opponent: "🇨🇮 Elfenbeinküste", tv: "ZDF" },
      { date: "25. Juni 2026", time: "22:00 Uhr", opponent: "🇪🇨 Ecuador", tv: "ARD/ZDF" },
    ];

    const groupColors = {
      A: "#e74c3c", B: "#e67e22", C: "#f1c40f", D: "#2ecc71",
      E: "#3498db", F: "#9b59b6", G: "#1abc9c", H: "#e91e8c",
      I: "#ff5722", J: "#607d8b", K: "#8bc34a", L: "#ff9800",
    };

    function App() {
      const [activeTab, setActiveTab] = useState("gruppen");
      const [selectedGroup, setSelectedGroup] = useState(null);

      const s = {
        page: { minHeight: "100vh", background: "linear-gradient(135deg, #0a0a1a 0%, #0d1b2a 50%, #0a1628 100%)", fontFamily: "Georgia, serif", color: "#e8e0d0" },
        header: { background: "linear-gradient(180deg, #c8a400 0%, #a07800 100%)", padding: "32px 24px 24px", textAlign: "center", position: "relative", overflow: "hidden" },
        headerPattern: { position: "absolute", inset: 0, backgroundImage: "repeating-linear-gradient(45deg, transparent, transparent 10px, rgba(0,0,0,0.05) 10px, rgba(0,0,0,0.05) 20px)" },
        subtitle: { fontSize: "13px", letterSpacing: "4px", color: "#3a2000", marginBottom: "8px", textTransform: "uppercase" },
        title: { fontSize: "clamp(36px, 8vw, 64px)", fontWeight: "900", color: "#1a0a00", margin: "0 0 4px", lineHeight: 1 },
        location: { fontSize: "14px", color: "#3a2000", letterSpacing: "3px" },
        meta: { marginTop: "12px", fontSize: "13px", color: "#3a2000" },
        tabs: { display: "flex", background: "#111827", borderBottom: "1px solid #2a3a50" },
        content: { padding: "24px 16px", maxWidth: "800px", margin: "0 auto" },
        hint: { color: "#8a9bb0", fontSize: "13px", textAlign: "center", marginBottom: "24px", letterSpacing: "1px" },
        footer: { textAlign: "center", padding: "24px", color: "#3a4a5a", fontSize: "11px", letterSpacing: "1px" },
      };

      return (
        <div style={s.page}>
          <div style={s.header}>
            <div style={s.headerPattern} />
            <div style={{ position: "relative" }}>
              <div style={s.subtitle}>FIFA Fußball-Weltmeisterschaft</div>
              <h1 style={s.title}>WM 2026</h1>
              <div style={s.location}>USA · KANADA · MEXIKO</div>
              <div style={s.meta}>48 Teams · 104 Spiele · 11. Juni – 19. Juli 2026</div>
            </div>
          </div>

          <div style={s.tabs}>
            {[
              { id: "gruppen", label: "Gruppen A–L" },
              { id: "spielplan", label: "Turnierphasen" },
              { id: "deutschland", label: "🇩🇪 Deutschland" },
            ].map(tab => (
              <button key={tab.id} onClick={() => setActiveTab(tab.id)} style={{
                flex: 1, padding: "14px 8px",
                background: activeTab === tab.id ? "#c8a400" : "transparent",
                color: activeTab === tab.id ? "#1a0a00" : "#8a9bb0",
                border: "none", cursor: "pointer", fontSize: "13px",
                fontWeight: activeTab === tab.id ? "700" : "400",
                letterSpacing: "1px", transition: "all 0.2s", fontFamily: "inherit",
              }}>{tab.label}</button>
            ))}
          </div>

          <div style={s.content}>
            {activeTab === "gruppen" && (
              <div>
                <p style={s.hint}>12 GRUPPEN · 4 TEAMS PRO GRUPPE · TOP 2 + BESTE 8 DRITTE WEITER</p>
                <div style={{ display: "grid", gap: "12px" }}>
                  {groups.map(group => (
                    <div key={group.id}
                      onClick={() => setSelectedGroup(selectedGroup === group.id ? null : group.id)}
                      style={{
                        background: selectedGroup === group.id ? `linear-gradient(135deg, ${groupColors[group.id]}22, #1a2535)` : "#111827",
                        border: `1px solid ${selectedGroup === group.id ? groupColors[group.id] : "#2a3a50"}`,
                        borderRadius: "8px", padding: "16px", cursor: "pointer", transition: "all 0.2s",
                      }}>
                      <div style={{ display: "flex", alignItems: "center", gap: "16px" }}>
                        <div style={{
                          width: "44px", height: "44px", background: groupColors[group.id],
                          borderRadius: "8px", display: "flex", alignItems: "center", justifyContent: "center",
                          fontSize: "22px", fontWeight: "900", color: "#fff", flexShrink: 0,
                        }}>{group.id}</div>
                        <div style={{ flex: 1 }}>
                          <div style={{ display: "flex", flexWrap: "wrap", gap: "8px" }}>
                            {group.teams.map((team, i) => (
                              <span key={i} style={{
                                background: i === 0 ? `${groupColors[group.id]}33` : "#1e2d40",
                                border: i === 0 ? `1px solid ${groupColors[group.id]}66` : "1px solid #2a3a50",
                                borderRadius: "4px", padding: "4px 10px", fontSize: "13px",
                                color: i === 0 ? "#e8e0d0" : "#a0b0c0", fontWeight: i === 0 ? "600" : "400",
                              }}>{team}</span>
                            ))}
                          </div>
                        </div>
                        <div style={{ color: "#4a6a80", fontSize: "18px" }}>{selectedGroup === group.id ? "▲" : "▼"}</div>
                      </div>
                      {selectedGroup === group.id && (
                        <div style={{ marginTop: "12px", paddingTop: "12px", borderTop: `1px solid ${groupColors[group.id]}44`, fontSize: "13px", color: "#8a9bb0", fontStyle: "italic" }}>
                          💬 {group.note}
                        </div>
                      )}
                    </div>
                  ))}
                </div>
              </div>
            )}

            {activeTab === "spielplan" && (
              <div>
                <p style={s.hint}>TURNIERPHASEN IM ÜBERBLICK</p>
                <div style={{ position: "relative" }}>
                  <div style={{ position: "absolute", left: "31px", top: 0, bottom: 0, width: "2px", background: "linear-gradient(180deg, #c8a400, #8a5200, #c8a400)" }} />
                  <div style={{ display: "flex", flexDirection: "column", gap: "16px" }}>
                    {rounds.map((round, i) => (
                      <div key={i} style={{ display: "flex", gap: "20px", alignItems: "flex-start" }}>
                        <div style={{
                          width: "44px", height: "44px",
                          background: round.name === "FINALE" ? "#c8a400" : "#1e2d40",
                          border: `2px solid ${round.name === "FINALE" ? "#c8a400" : "#2a3a50"}`,
                          borderRadius: "50%", display: "flex", alignItems: "center", justifyContent: "center",
                          fontSize: round.icon.length > 2 ? "18px" : "11px", fontWeight: "900",
                          color: round.name === "FINALE" ? "#1a0a00" : "#8a9bb0", flexShrink: 0, zIndex: 1,
                        }}>{round.icon}</div>
                        <div style={{
                          flex: 1,
                          background: round.name === "FINALE" ? "linear-gradient(135deg, #c8a40022, #1a2535)" : "#111827",
                          border: `1px solid ${round.name === "FINALE" ? "#c8a40066" : "#2a3a50"}`,
                          borderRadius: "8px", padding: "14px 16px",
                        }}>
                          <div style={{ fontWeight: "700", fontSize: round.name === "FINALE" ? "18px" : "15px", color: round.name === "FINALE" ? "#c8a400" : "#e8e0d0", letterSpacing: round.name === "FINALE" ? "2px" : "0" }}>{round.name}</div>
                          <div style={{ fontSize: "13px", color: "#6a8a9a", marginTop: "4px" }}>📅 {round.dates}</div>
                          {round.extra && <div style={{ fontSize: "12px", color: round.name === "FINALE" ? "#c8a400" : "#6a8a9a", marginTop: "6px" }}>{round.extra}</div>}
                        </div>
                      </div>
                    ))}
                  </div>
                </div>
                <div style={{ marginTop: "24px", background: "#111827", border: "1px solid #2a3a50", borderRadius: "8px", padding: "16px" }}>
                  <div style={{ fontWeight: "700", marginBottom: "8px", color: "#c8a400" }}>Neuer Modus 2026</div>
                  <div style={{ fontSize: "13px", color: "#8a9bb0", lineHeight: "1.8" }}>
                    • 48 Nationen in 12 Vierergruppen (A–L)<br />
                    • Top 2 jeder Gruppe + beste 8 Gruppendritte = 32 Teams weiter<br />
                    • Erstmals Sechzehntelfinale in der WM-Geschichte<br />
                    • Insgesamt 104 Spiele in 39 Tagen
                  </div>
                </div>
              </div>
            )}

            {activeTab === "deutschland" && (
              <div>
                <div style={{ background: "linear-gradient(135deg, #3498db22, #1a2535)", border: "1px solid #3498db66", borderRadius: "8px", padding: "20px", marginBottom: "20px", textAlign: "center" }}>
                  <div style={{ fontSize: "40px", marginBottom: "8px" }}>🇩🇪</div>
                  <div style={{ fontSize: "22px", fontWeight: "700", color: "#e8e0d0" }}>Deutschland</div>
                  <div style={{ display: "inline-block", background: "#3498db", borderRadius: "20px", padding: "4px 16px", fontSize: "13px", fontWeight: "700", color: "#fff", marginTop: "8px", letterSpacing: "2px" }}>GRUPPE E</div>
                  <div style={{ marginTop: "8px", fontSize: "13px", color: "#8a9bb0" }}>Trainer: Julian Nagelsmann · FIFA-Rang 9</div>
                </div>

                <div style={{ fontWeight: "700", marginBottom: "12px", color: "#c8a400", letterSpacing: "2px", fontSize: "13px" }}>GRUPPENSPIELE</div>
                {germanyGames.map((game, i) => (
                  <div key={i} style={{ background: "#111827", border: "1px solid #2a3a50", borderRadius: "8px", padding: "16px", marginBottom: "10px", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                    <div>
                      <div style={{ fontSize: "14px", fontWeight: "600", color: "#e8e0d0", marginBottom: "4px" }}>🇩🇪 Deutschland vs. {game.opponent}</div>
                      <div style={{ fontSize: "12px", color: "#6a8a9a" }}>📅 {game.date} · ⏰ {game.time}</div>
                    </div>
                    <div style={{ background: "#1e2d40", border: "1px solid #2a3a50", borderRadius: "4px", padding: "4px 10px", fontSize: "12px", color: "#c8a400", fontWeight: "700" }}>{game.tv}</div>
                  </div>
                ))}

                <div style={{ background: "#111827", border: "1px solid #2a3a50", borderRadius: "8px", padding: "16px", marginTop: "16px" }}>
                  <div style={{ fontWeight: "700", marginBottom: "12px", color: "#c8a400", fontSize: "13px" }}>GRUPPE E – ALLE TEAMS</div>
                  {["🇩🇪 Deutschland (Favorit)", "🇨🇮 Elfenbeinküste (Afrika-Cup-Sieger 2024)", "🇪🇨 Ecuador (CONMEBOL-Zweiter)", "🇨🇼 Curaçao (WM-Debüt)"].map((team, i) => (
                    <div key={i} style={{ display: "flex", alignItems: "center", gap: "12px", padding: "10px 0", borderBottom: i < 3 ? "1px solid #1e2d40" : "none" }}>
                      <div style={{ width: "24px", height: "24px", background: i === 0 ? "#3498db" : "#1e2d40", borderRadius: "50%", display: "flex", alignItems: "center", justifyContent: "center", fontSize: "12px", fontWeight: "700", color: "#e8e0d0", flexShrink: 0 }}>{i + 1}</div>
                      <span style={{ fontSize: "14px", color: i === 0 ? "#e8e0d0" : "#8a9bb0" }}>{team}</span>
                    </div>
                  ))}
                </div>

                <div style={{ marginTop: "16px", background: "linear-gradient(135deg, #c8a40011, #1a2535)", border: "1px solid #c8a40044", borderRadius: "8px", padding: "16px", fontSize: "13px", color: "#8a9bb0", lineHeight: "1.8" }}>
                  <span style={{ color: "#c8a400", fontWeight: "700" }}>Turnierpfad: </span>
                  Als Gruppensieger geht es im Sechzehntelfinale gegen einen Gruppendritten aus den Gruppen A, B, C, D oder F. Deutschland und Brasilien befinden sich auf derselben Bracket-Hälfte — ein mögliches Viertelfinale.
                </div>
              </div>
            )}
          </div>

          <div style={s.footer}>FIFA WM 2026 · USA · KANADA · MEXIKO · FINALE 19. JULI 2026</div>
        </div>
      );
    }

    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(<App />);
  </script>
</body>
</html>
HTMLEOF
echo "done"
