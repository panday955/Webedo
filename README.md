# Webedo
I want to develop my projects 

import { useState, useRef, useCallback } from "react";

const COLORS = {
  navy: "#0A1628",
  navyCard: "#111D2E",
  navyLight: "#162236",
  gold: "#C9A04A",
  goldLight: "#E8C76A",
  goldDim: "#8A6D30",
  champagne: "#F5EDD3",
  white: "#FFFFFF",
  gray: "#8A9BB0",
  grayLight: "#C2CDD8",
  red: "#E05555",
  green: "#4CAF7D",
  blue: "#4A90D9",
  purple: "#8B5CF6",
};

const initialClients = [
  { id: 1, name: "Priya Sharma", email: "priya@email.com", phone: "+91 98765 43210", events: 3, photos: 240, status: "active", joined: "Jan 2024", avatar: "PS" },
  { id: 2, name: "Rahul & Meera", email: "rahul@email.com", phone: "+91 87654 32109", events: 1, photos: 512, status: "active", joined: "Mar 2024", avatar: "RM" },
  { id: 3, name: "Anjali Verma", email: "anjali@email.com", phone: "+91 76543 21098", events: 2, photos: 186, status: "pending", joined: "Apr 2024", avatar: "AV" },
  { id: 4, name: "Karthik Studios", email: "karthik@studio.com", phone: "+91 65432 10987", events: 5, photos: 890, status: "active", joined: "Nov 2023", avatar: "KS" },
  { id: 5, name: "Deepa Nair", email: "deepa@email.com", phone: "+91 54321 09876", events: 1, photos: 95, status: "completed", joined: "May 2024", avatar: "DN" },
];

const initialEvents = [
  { id: 1, name: "Priya's Wedding Shoot", client: "Priya Sharma", type: "Wedding", date: "2024-06-15", status: "completed", photos: 240, videos: 3, size: "4.2 GB" },
  { id: 2, name: "Rahul & Meera - Engagement", client: "Rahul & Meera", type: "Engagement", date: "2024-06-22", status: "active", photos: 512, videos: 7, size: "8.1 GB" },
  { id: 3, name: "Anjali Maternity Session", client: "Anjali Verma", type: "Maternity", date: "2024-07-01", status: "upcoming", photos: 0, videos: 0, size: "0 GB" },
  { id: 4, name: "Karthik Corporate Portraits", client: "Karthik Studios", type: "Corporate", date: "2024-05-30", status: "completed", photos: 890, videos: 2, size: "6.7 GB" },
  { id: 5, name: "Deepa Baby Shower", client: "Deepa Nair", type: "Birthday", date: "2024-06-28", status: "active", photos: 95, videos: 1, size: "1.8 GB" },
];

const initialMedia = [
  { id: 1, name: "DSC_0012.jpg", type: "photo", client: "Priya Sharma", event: "Priya's Wedding Shoot", size: "4.2 MB", date: "2024-06-15", color: "#C9A04A" },
  { id: 2, name: "VID_0001.mp4", type: "video", client: "Rahul & Meera", event: "Rahul & Meera - Engagement", size: "1.2 GB", date: "2024-06-22", color: "#4A90D9" },
  { id: 3, name: "DSC_0047.jpg", type: "photo", client: "Karthik Studios", event: "Corporate Portraits", size: "3.8 MB", date: "2024-05-30", color: "#4CAF7D" },
  { id: 4, name: "DSC_0089.jpg", type: "photo", client: "Priya Sharma", event: "Priya's Wedding Shoot", size: "5.1 MB", date: "2024-06-15", color: "#8B5CF6" },
  { id: 5, name: "VID_0002.mp4", type: "video", client: "Deepa Nair", event: "Baby Shower", size: "890 MB", date: "2024-06-28", color: "#E05555" },
  { id: 6, name: "DSC_0124.jpg", type: "photo", client: "Anjali Verma", event: "Maternity Session", size: "4.7 MB", date: "2024-04-20", color: "#E8C76A" },
  { id: 7, name: "DSC_0200.jpg", type: "photo", client: "Rahul & Meera", event: "Engagement", size: "3.2 MB", date: "2024-06-22", color: "#C9A04A" },
  { id: 8, name: "VID_0003.mp4", type: "video", client: "Karthik Studios", event: "Corporate Portraits", size: "2.1 GB", date: "2024-05-30", color: "#4A90D9" },
];

const NAV_ITEMS = [
  { id: "dashboard", label: "Dashboard", icon: "⊞" },
  { id: "upload", label: "Upload Media", icon: "↑" },
  { id: "gallery", label: "Gallery", icon: "⊟" },
  { id: "events", label: "Events", icon: "◈" },
  { id: "clients", label: "Clients", icon: "◎" },
  { id: "analytics", label: "Analytics", icon: "▦" },
  { id: "settings", label: "Settings", icon: "⚙" },
];

function StatCard({ label, value, sub, color, icon }) {
  return (
    <div style={{
      background: COLORS.navyCard,
      borderRadius: 16,
      padding: "24px",
      border: `1px solid rgba(201,160,74,0.12)`,
      position: "relative",
      overflow: "hidden",
      flex: 1,
      minWidth: 160,
    }}>
      <div style={{
        position: "absolute", top: -20, right: -20,
        width: 80, height: 80, borderRadius: "50%",
        background: `${color}15`,
      }} />
      <div style={{ fontSize: 28, marginBottom: 8 }}>{icon}</div>
      <div style={{ fontSize: 28, fontWeight: 700, color: COLORS.white, fontFamily: "'Playfair Display', serif", lineHeight: 1 }}>{value}</div>
      <div style={{ fontSize: 13, color: COLORS.gray, marginTop: 6 }}>{label}</div>
      {sub && <div style={{ fontSize: 12, color, marginTop: 4, fontWeight: 600 }}>{sub}</div>}
    </div>
  );
}

function Badge({ status }) {
  const map = {
    active: { bg: "#4CAF7D20", color: "#4CAF7D", label: "Active" },
    completed: { bg: "#C9A04A20", color: "#C9A04A", label: "Completed" },
    pending: { bg: "#4A90D920", color: "#4A90D9", label: "Pending" },
    upcoming: { bg: "#8B5CF620", color: "#8B5CF6", label: "Upcoming" },
  };
  const s = map[status] || map.active;
  return (
    <span style={{
      background: s.bg, color: s.color,
      padding: "3px 10px", borderRadius: 20,
      fontSize: 11, fontWeight: 700, letterSpacing: 0.5,
    }}>{s.label}</span>
  );
}

function Dashboard({ clients, events, media }) {
  const totalPhotos = media.filter(m => m.type === "photo").length;
  const totalVideos = media.filter(m => m.type === "video").length;
  const recentEvents = [...events].sort((a, b) => new Date(b.date) - new Date(a.date)).slice(0, 4);

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 28 }}>
      <div>
        <h2 style={{ fontFamily: "'Playfair Display', serif", fontSize: 28, color: COLORS.white, margin: 0 }}>Good morning ✨</h2>
        <p style={{ color: COLORS.gray, marginTop: 4, fontSize: 14 }}>Here's what's happening at CL Photography today.</p>
      </div>

      {/* Stats */}
      <div style={{ display: "flex", gap: 16, flexWrap: "wrap" }}>
        <StatCard label="Total Clients" value={clients.length} sub="+2 this month" color={COLORS.gold} icon="👥" />
        <StatCard label="Events" value={events.length} sub="2 active now" color={COLORS.blue} icon="📅" />
        <StatCard label="Photos" value={`${totalPhotos * 30}+`} sub="12 uploaded today" color={COLORS.green} icon="📸" />
        <StatCard label="Videos" value={`${totalVideos * 4}`} sub="3.4 GB today" color={COLORS.purple} icon="🎬" />
      </div>

      {/* Storage Bar */}
      <div style={{ background: COLORS.navyCard, borderRadius: 16, padding: 24, border: "1px solid rgba(201,160,74,0.12)" }}>
        <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 12 }}>
          <span style={{ color: COLORS.white, fontWeight: 600 }}>Storage Usage</span>
          <span style={{ color: COLORS.gold, fontWeight: 700 }}>68.4 GB / 100 GB</span>
        </div>
        <div style={{ background: COLORS.navyLight, borderRadius: 8, height: 10, overflow: "hidden" }}>
          <div style={{
            width: "68.4%", height: "100%", borderRadius: 8,
            background: `linear-gradient(90deg, ${COLORS.gold}, ${COLORS.goldLight})`,
            transition: "width 0.6s ease",
          }} />
        </div>
        <div style={{ display: "flex", gap: 20, marginTop: 14, flexWrap: "wrap" }}>
          {[
            { label: "Photos", val: "24.1 GB", color: COLORS.gold },
            { label: "Videos", val: "38.2 GB", color: COLORS.blue },
            { label: "Raw Files", val: "6.1 GB", color: COLORS.purple },
          ].map(s => (
            <div key={s.label} style={{ display: "flex", alignItems: "center", gap: 6 }}>
              <div style={{ width: 8, height: 8, borderRadius: "50%", background: s.color }} />
              <span style={{ fontSize: 12, color: COLORS.gray }}>{s.label}</span>
              <span style={{ fontSize: 12, color: COLORS.white, fontWeight: 600 }}>{s.val}</span>
            </div>
          ))}
        </div>
      </div>

      {/* Recent Events & Quick Actions */}
      <div style={{ display: "grid", gridTemplateColumns: "1fr 340px", gap: 20 }}>
        <div style={{ background: COLORS.navyCard, borderRadius: 16, padding: 24, border: "1px solid rgba(201,160,74,0.12)" }}>
          <h3 style={{ color: COLORS.white, margin: "0 0 16px", fontFamily: "'Playfair Display', serif", fontSize: 18 }}>Recent Events</h3>
          <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
            {recentEvents.map(ev => (
              <div key={ev.id} style={{
                display: "flex", alignItems: "center", gap: 14,
                padding: "12px 16px", background: COLORS.navyLight, borderRadius: 12,
              }}>
                <div style={{
                  width: 40, height: 40, borderRadius: 10, background: `${COLORS.gold}20`,
                  display: "flex", alignItems: "center", justifyContent: "center",
                  fontSize: 18,
                }}>
                  {ev.type === "Wedding" ? "💒" : ev.type === "Engagement" ? "💍" : ev.type === "Maternity" ? "👶" : ev.type === "Corporate" ? "🏢" : "🎂"}
                </div>
                <div style={{ flex: 1 }}>
                  <div style={{ color: COLORS.white, fontWeight: 600, fontSize: 14 }}>{ev.name}</div>
                  <div style={{ color: COLORS.gray, fontSize: 12, marginTop: 2 }}>{ev.client} · {ev.date}</div>
                </div>
                <div style={{ textAlign: "right" }}>
                  <Badge status={ev.status} />
                  <div style={{ color: COLORS.gray, fontSize: 11, marginTop: 4 }}>{ev.size}</div>
                </div>
              </div>
            ))}
          </div>
        </div>

        {/* Quick Upload + Activity */}
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <div style={{
            background: `linear-gradient(135deg, ${COLORS.gold}20, ${COLORS.goldDim}15)`,
            border: `1px solid ${COLORS.gold}40`,
            borderRadius: 16, padding: 24,
          }}>
            <div style={{ fontSize: 32, marginBottom: 8 }}>⬆️</div>
            <h4 style={{ color: COLORS.gold, margin: "0 0 6px", fontFamily: "'Playfair Display', serif" }}>Quick Upload</h4>
            <p style={{ color: COLORS.grayLight, fontSize: 13, margin: "0 0 16px" }}>Drag & drop photos and videos from today's shoot</p>
            <div style={{
              background: COLORS.gold, color: COLORS.navy, padding: "10px 20px",
              borderRadius: 8, fontWeight: 700, fontSize: 13, cursor: "pointer", textAlign: "center",
            }}>Upload Now →</div>
          </div>

          <div style={{ background: COLORS.navyCard, borderRadius: 16, padding: 20, border: "1px solid rgba(201,160,74,0.12)", flex: 1 }}>
            <h4 style={{ color: COLORS.white, margin: "0 0 14px", fontSize: 15, fontWeight: 600 }}>Today's Activity</h4>
            {[
              { text: "12 photos uploaded", time: "10 min ago", icon: "📸" },
              { text: "Deepa's gallery shared", time: "1 hr ago", icon: "🔗" },
              { text: "New client: Anjali", time: "3 hr ago", icon: "✨" },
              { text: "Invoice sent to Karthik", time: "Yesterday", icon: "📄" },
            ].map((a, i) => (
              <div key={i} style={{ display: "flex", gap: 10, alignItems: "flex-start", marginBottom: 12 }}>
                <span style={{ fontSize: 16 }}>{a.icon}</span>
                <div style={{ flex: 1 }}>
                  <div style={{ color: COLORS.grayLight, fontSize: 13 }}>{a.text}</div>
                  <div style={{ color: COLORS.gray, fontSize: 11, marginTop: 2 }}>{a.time}</div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
}

function UploadPage({ media, setMedia }) {
  const [dragging, setDragging] = useState(false);
  const [uploads, setUploads] = useState([]);
  const [selectedClient, setSelectedClient] = useState("");
  const [selectedEvent, setSelectedEvent] = useState("");
  const fileRef = useRef();

  const simulateUpload = (files) => {
    const newUploads = Array.from(files).map((f, i) => ({
      id: Date.now() + i,
      name: f.name,
      size: (f.size / (1024 * 1024)).toFixed(1) + " MB",
      type: f.type.startsWith("video") ? "video" : "photo",
      progress: 0,
      status: "uploading",
    }));
    setUploads(prev => [...newUploads, ...prev]);

    newUploads.forEach(u => {
      let p = 0;
      const interval = setInterval(() => {
        p += Math.random() * 18 + 4;
        if (p >= 100) {
          p = 100;
          clearInterval(interval);
          setUploads(prev => prev.map(x => x.id === u.id ? { ...x, progress: 100, status: "done" } : x));
          setMedia(prev => [{
            id: Date.now(),
            name: u.name,
            type: u.type,
            client: selectedClient || "Unassigned",
            event: selectedEvent || "Unassigned",
            size: u.size,
            date: new Date().toISOString().split("T")[0],
            color: COLORS.gold,
          }, ...prev]);
        } else {
          setUploads(prev => prev.map(x => x.id === u.id ? { ...x, progress: Math.round(p) } : x));
        }
      }, 180);
    });
  };

  const onDrop = useCallback((e) => {
    e.preventDefault();
    setDragging(false);
    simulateUpload(e.dataTransfer.files);
  }, [selectedClient, selectedEvent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 24 }}>
      <div>
        <h2 style={{ fontFamily: "'Playfair Display', serif", fontSize: 28, color: COLORS.white, margin: 0 }}>Upload Media</h2>
        <p style={{ color: COLORS.gray, fontSize: 14, marginTop: 4 }}>Upload photos and videos — supports up to 5 GB per file</p>
      </div>

      {/* Assignment */}
      <div style={{ display: "flex", gap: 16 }}>
        {[
          { label: "Assign to Client", value: selectedClient, set: setSelectedClient, opts: ["Priya Sharma", "Rahul & Meera", "Anjali Verma", "Karthik Studios", "Deepa Nair"] },
          { label: "Assign to Event", value: selectedEvent, set: setSelectedEvent, opts: ["Priya's Wedding Shoot", "Rahul & Meera - Engagement", "Anjali Maternity Session", "Corporate Portraits", "Baby Shower"] },
        ].map(f => (
          <div key={f.label} style={{ flex: 1 }}>
            <label style={{ color: COLORS.gray, fontSize: 12, fontWeight: 600, letterSpacing: 0.5, display: "block", marginBottom: 6 }}>{f.label.toUpperCase()}</label>
            <select
              value={f.value}
              onChange={e => f.set(e.target.value)}
              style={{
                width: "100%", background: COLORS.navyCard, border: `1px solid rgba(201,160,74,0.25)`,
                color: COLORS.white, padding: "10px 14px", borderRadius: 10, fontSize: 14, outline: "none",
              }}
            >
              <option value="">Select…</option>
              {f.opts.map(o => <option key={o}>{o}</option>)}
            </select>
          </div>
        ))}
      </div>

      {/* Drop Zone */}
      <div
        onDragOver={e => { e.preventDefault(); setDragging(true); }}
        onDragLeave={() => setDragging(false)}
        onDrop={onDrop}
        onClick={() => fileRef.current.click()}
        style={{
          border: `2px dashed ${dragging ? COLORS.gold : "rgba(201,160,74,0.35)"}`,
          borderRadius: 20,
          padding: "60px 40px",
          textAlign: "center",
          cursor: "pointer",
          background: dragging ? `${COLORS.gold}08` : COLORS.navyCard,
          transition: "all 0.25s",
          position: "relative",
          overflow: "hidden",
        }}
      >
        {dragging && (
          <div style={{
            position: "absolute", inset: 0,
            background: `radial-gradient(circle at center, ${COLORS.gold}15 0%, transparent 70%)`,
            pointerEvents: "none",
          }} />
        )}
        <input ref={fileRef} type="file" multiple accept="image/*,video/*" style={{ display: "none" }}
          onChange={e => simulateUpload(e.target.files)} />
        <div style={{ fontSize: 52, marginBottom: 16 }}>🎞</div>
        <div style={{ fontSize: 20, fontWeight: 700, color: COLORS.white, fontFamily: "'Playfair Display', serif", marginBottom: 8 }}>
          Drop your files here
        </div>
        <div style={{ color: COLORS.gray, fontSize: 14 }}>JPG, PNG, RAW, MP4, MOV · Up to 5 GB per file</div>
        <div style={{
          marginTop: 20, display: "inline-block",
          background: `linear-gradient(135deg, ${COLORS.gold}, ${COLORS.goldLight})`,
          color: COLORS.navy, padding: "10px 28px", borderRadius: 8, fontWeight: 700, fontSize: 14,
        }}>Browse Files</div>
      </div>

      {/* Upload Queue */}
      {uploads.length > 0 && (
        <div style={{ background: COLORS.navyCard, borderRadius: 16, padding: 20, border: "1px solid rgba(201,160,74,0.12)" }}>
          <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 16 }}>
            <h3 style={{ color: COLORS.white, margin: 0, fontSize: 16, fontWeight: 600 }}>Upload Queue</h3>
            <span style={{ color: COLORS.gray, fontSize: 13 }}>{uploads.filter(u => u.status === "done").length}/{uploads.length} completed</span>
          </div>
          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            {uploads.map(u => (
              <div key={u.id} style={{
                background: COLORS.navyLight, borderRadius: 12, padding: "12px 16px",
                display: "flex", alignItems: "center", gap: 14,
              }}>
                <span style={{ fontSize: 22 }}>{u.type === "video" ? "🎬" : "📸"}</span>
                <div style={{ flex: 1 }}>
                  <div style={{ display: "flex", justifyContent: "space-between" }}>
                    <span style={{ color: COLORS.white, fontSize: 13, fontWeight: 600 }}>{u.name}</span>
                    <span style={{ color: COLORS.gray, fontSize: 12 }}>{u.size}</span>
                  </div>
                  <div style={{ marginTop: 6, background: "#1a2a3a", borderRadius: 4, height: 5, overflow: "hidden" }}>
                    <div style={{
                      width: `${u.progress}%`, height: "100%", borderRadius: 4,
                      background: u.status === "done"
                        ? `linear-gradient(90deg, ${COLORS.green}, #6FCF97)`
                        : `linear-gradient(90deg, ${COLORS.gold}, ${COLORS.goldLight})`,
                      transition: "width 0.3s",
                    }} />
                  </div>
                  <div style={{ display: "flex", justifyContent: "space-between", marginTop: 4 }}>
                    <span style={{ color: COLORS.gray, fontSize: 11 }}>
                      {u.status === "done" ? "✓ Upload complete" : `Uploading… ${u.progress}%`}
                    </span>
                    {u.status === "done" && <span style={{ color: COLORS.green, fontSize: 11 }}>✓</span>}
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
}

function GalleryPage({ media, setMedia }) {
  const [filter, setFilter] = useState("all");
  const [search, setSearch] = useState("");
  const [view, setView] = useState("grid");

  const filtered = media.filter(m => {
    const matchType = filter === "all" || m.type === filter;
    const matchSearch = m.name.toLowerCase().includes(search.toLowerCase()) ||
      m.client.toLowerCase().includes(search.toLowerCase());
    return matchType && matchSearch;
  });

  const heights = [200, 260, 180, 240, 220, 200, 280, 200];

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 24 }}>
      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-end", flexWrap: "wrap", gap: 12 }}>
        <div>
          <h2 style={{ fontFamily: "'Playfair Display', serif", fontSize: 28, color: COLORS.white,
