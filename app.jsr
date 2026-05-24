import { useState } from "react";

const initialOrders = [
  { id: "FF-001", customer: "Ayesha Khan", item: "Gold Necklace", amount: 4500, status: "Delivered", date: "2026-05-20" },
  { id: "FF-002", customer: "Sara Ahmed", item: "Diamond Ring", amount: 12000, status: "Pending", date: "2026-05-22" },
  { id: "FF-003", customer: "Fatima Ali", item: "Pearl Earrings", amount: 2800, status: "Processing", date: "2026-05-23" },
];

const initialEmployees = [
  { id: "E-001", name: "Usman Malik", role: "Store Manager", phone: "0300-1234567", salary: 55000, status: "Active" },
  { id: "E-002", name: "Zara Hussain", role: "Sales Executive", phone: "0321-9876543", salary: 35000, status: "Active" },
  { id: "E-003", name: "Bilal Raza", role: "Cashier", phone: "0333-4567890", salary: 28000, status: "On Leave" },
];

const statusColors = {
  Delivered: "#22c55e",
  Pending: "#f59e0b",
  Processing: "#3b82f6",
  Cancelled: "#ef4444",
  Active: "#22c55e",
  "On Leave": "#f59e0b",
  Inactive: "#ef4444",
};

export default function FancyFinds() {
  const [tab, setTab] = useState("dashboard");
  const [orders, setOrders] = useState(initialOrders);
  const [employees, setEmployees] = useState(initialEmployees);
  const [showOrderForm, setShowOrderForm] = useState(false);
  const [showEmpForm, setShowEmpForm] = useState(false);
  const [orderForm, setOrderForm] = useState({ customer: "", item: "", amount: "", status: "Pending", date: "" });
  const [empForm, setEmpForm] = useState({ name: "", role: "", phone: "", salary: "", status: "Active" });
  const [search, setSearch] = useState("");
  const [editOrderId, setEditOrderId] = useState(null);
  const [editEmpId, setEditEmpId] = useState(null);
  const [deleteConfirm, setDeleteConfirm] = useState(null);

  const totalRevenue = orders.filter(o => o.status === "Delivered").reduce((s, o) => s + Number(o.amount), 0);
  const pendingOrders = orders.filter(o => o.status === "Pending").length;
  const activeEmps = employees.filter(e => e.status === "Active").length;

  function handleAddOrder() {
    if (!orderForm.customer || !orderForm.item || !orderForm.amount || !orderForm.date) return;
    if (editOrderId) {
      setOrders(orders.map(o => o.id === editOrderId ? { ...o, ...orderForm, amount: Number(orderForm.amount) } : o));
      setEditOrderId(null);
    } else {
      const newId = "FF-" + String(orders.length + 1).padStart(3, "0");
      setOrders([...orders, { id: newId, ...orderForm, amount: Number(orderForm.amount) }]);
    }
    setOrderForm({ customer: "", item: "", amount: "", status: "Pending", date: "" });
    setShowOrderForm(false);
  }

  function handleAddEmp() {
    if (!empForm.name || !empForm.role || !empForm.phone || !empForm.salary) return;
    if (editEmpId) {
      setEmployees(employees.map(e => e.id === editEmpId ? { ...e, ...empForm, salary: Number(empForm.salary) } : e));
      setEditEmpId(null);
    } else {
      const newId = "E-" + String(employees.length + 1).padStart(3, "0");
      setEmployees([...employees, { id: newId, ...empForm, salary: Number(empForm.salary) }]);
    }
    setEmpForm({ name: "", role: "", phone: "", salary: "", status: "Active" });
    setShowEmpForm(false);
  }

  function startEditOrder(o) {
    setOrderForm({ customer: o.customer, item: o.item, amount: o.amount, status: o.status, date: o.date });
    setEditOrderId(o.id);
    setShowOrderForm(true);
  }

  function startEditEmp(e) {
    setEmpForm({ name: e.name, role: e.role, phone: e.phone, salary: e.salary, status: e.status });
    setEditEmpId(e.id);
    setShowEmpForm(true);
  }

  function confirmDelete(type, id) {
    setDeleteConfirm({ type, id });
  }

  function doDelete() {
    if (!deleteConfirm) return;
    if (deleteConfirm.type === "order") setOrders(orders.filter(o => o.id !== deleteConfirm.id));
    else setEmployees(employees.filter(e => e.id !== deleteConfirm.id));
    setDeleteConfirm(null);
  }

  const filteredOrders = orders.filter(o =>
    o.customer.toLowerCase().includes(search.toLowerCase()) ||
    o.item.toLowerCase().includes(search.toLowerCase()) ||
    o.id.toLowerCase().includes(search.toLowerCase())
  );

  const filteredEmps = employees.filter(e =>
    e.name.toLowerCase().includes(search.toLowerCase()) ||
    e.role.toLowerCase().includes(search.toLowerCase()) ||
    e.id.toLowerCase().includes(search.toLowerCase())
  );

  const inputStyle = {
    width: "100%", padding: "10px 14px", borderRadius: 10,
    border: "1.5px solid #e2c97e", background: "#fff9ee",
    fontFamily: "Cormorant Garamond, serif", fontSize: 15, color: "#3d2b00",
    outline: "none", marginBottom: 10, boxSizing: "border-box"
  };

  const btnPrimary = {
    background: "linear-gradient(135deg, #c9a84c, #e8c96d)",
    color: "#3d2b00", border: "none", borderRadius: 10,
    padding: "10px 22px", fontWeight: 700, fontFamily: "Cormorant Garamond, serif",
    fontSize: 15, cursor: "pointer", boxShadow: "0 2px 8px #c9a84c55"
  };

  const btnGhost = {
    background: "transparent", color: "#9a7d2e", border: "1.5px solid #e2c97e",
    borderRadius: 10, padding: "8px 16px", fontWeight: 600,
    fontFamily: "Cormorant Garamond, serif", fontSize: 14, cursor: "pointer"
  };

  return (
    <div style={{ minHeight: "100vh", background: "linear-gradient(160deg, #fdf6e3 0%, #fef9f0 60%, #fdf0d5 100%)", fontFamily: "Cormorant Garamond, serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600;700&family=Playfair+Display:wght@700;900&display=swap');
        * { box-sizing: border-box; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-thumb { background: #e2c97e; border-radius: 4px; }
        .nav-btn { transition: all 0.2s; }
        .nav-btn:hover { background: #fef3d0 !important; }
        .row-hover:hover { background: #fef9ee !important; transition: background 0.15s; }
        .action-btn { opacity: 0.7; transition: opacity 0.2s; }
        .action-btn:hover { opacity: 1; }
        .card-stat:hover { transform: translateY(-2px); box-shadow: 0 8px 32px #c9a84c33 !important; transition: all 0.2s; }
        select option { background: #fff9ee; color: #3d2b00; }
      `}</style>

      {/* HEADER */}
      <div style={{ background: "linear-gradient(135deg, #3d2b00 0%, #6b4c00 100%)", padding: "0 32px", display: "flex", alignItems: "center", justifyContent: "space-between", boxShadow: "0 4px 24px #3d2b0044" }}>
        <div style={{ display: "flex", alignItems: "center", gap: 14, padding: "18px 0" }}>
          <div style={{ width: 44, height: 44, background: "linear-gradient(135deg, #c9a84c, #e8c96d)", borderRadius: "50%", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 22 }}>✦</div>
          <div>
            <div style={{ fontFamily: "Playfair Display, serif", fontSize: 24, fontWeight: 900, color: "#e8c96d", letterSpacing: 1 }}>Fancy Finds</div>
            <div style={{ color: "#c9a84c88", fontSize: 12, letterSpacing: 2, textTransform: "uppercase" }}>Store Management</div>
          </div>
        </div>
        <div style={{ display: "flex", gap: 4 }}>
          {["dashboard", "orders", "employees"].map(t => (
            <button key={t} className="nav-btn" onClick={() => { setTab(t); setSearch(""); setShowOrderForm(false); setShowEmpForm(false); }}
              style={{ background: tab === t ? "#e8c96d22" : "transparent", color: tab === t ? "#e8c96d" : "#c9a84c", border: tab === t ? "1px solid #e8c96d44" : "1px solid transparent", borderRadius: 8, padding: "8px 20px", cursor: "pointer", fontFamily: "Cormorant Garamond, serif", fontSize: 15, fontWeight: 600, textTransform: "capitalize", letterSpacing: 0.5 }}>
              {t === "dashboard" ? "🏠 Dashboard" : t === "orders" ? "📦 Orders" : "👥 Employees"}
            </button>
          ))}
        </div>
      </div>

      <div style={{ maxWidth: 1100, margin: "0 auto", padding: "32px 20px" }}>

        {/* DASHBOARD */}
        {tab === "dashboard" && (
          <div>
            <div style={{ marginBottom: 28 }}>
              <div style={{ fontFamily: "Playfair Display, serif", fontSize: 30, fontWeight: 900, color: "#3d2b00" }}>Aapka Dashboard</div>
              <div style={{ color: "#9a7d2e", fontSize: 15 }}>Fancy Finds store ka overview</div>
            </div>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(220px, 1fr))", gap: 20, marginBottom: 36 }}>
              {[
                { label: "Total Orders", value: orders.length, icon: "📦", color: "#3b82f6" },
                { label: "Total Revenue", value: `Rs. ${totalRevenue.toLocaleString()}`, icon: "💰", color: "#22c55e" },
                { label: "Pending Orders", value: pendingOrders, icon: "⏳", color: "#f59e0b" },
                { label: "Active Staff", value: activeEmps, icon: "👥", color: "#8b5cf6" },
              ].map(s => (
                <div key={s.label} className="card-stat" style={{ background: "#fff", borderRadius: 16, padding: "24px 20px", border: "1.5px solid #e2c97e", boxShadow: "0 2px 12px #c9a84c22", cursor: "default" }}>
                  <div style={{ fontSize: 32, marginBottom: 8 }}>{s.icon}</div>
                  <div style={{ fontSize: 26, fontWeight: 700, color: s.color, fontFamily: "Playfair Display, serif" }}>{s.value}</div>
                  <div style={{ color: "#9a7d2e", fontSize: 14, marginTop: 4 }}>{s.label}</div>
                </div>
              ))}
            </div>

            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
              <div style={{ background: "#fff", borderRadius: 16, border: "1.5px solid #e2c97e", padding: 24 }}>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 18, color: "#3d2b00", marginBottom: 16, fontWeight: 700 }}>Latest Orders</div>
                {orders.slice(-3).reverse().map(o => (
                  <div key={o.id} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "10px 0", borderBottom: "1px solid #f5e6c0" }}>
                    <div>
                      <div style={{ fontWeight: 600, color: "#3d2b00", fontSize: 15 }}>{o.customer}</div>
                      <div style={{ color: "#9a7d2e", fontSize: 13 }}>{o.item} — {o.id}</div>
                    </div>
                    <span style={{ background: statusColors[o.status] + "22", color: statusColors[o.status], borderRadius: 8, padding: "3px 12px", fontSize: 13, fontWeight: 600 }}>{o.status}</span>
                  </div>
                ))}
              </div>
              <div style={{ background: "#fff", borderRadius: 16, border: "1.5px solid #e2c97e", padding: 24 }}>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 18, color: "#3d2b00", marginBottom: 16, fontWeight: 700 }}>Staff Overview</div>
                {employees.map(e => (
                  <div key={e.id} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "10px 0", borderBottom: "1px solid #f5e6c0" }}>
                    <div>
                      <div style={{ fontWeight: 600, color: "#3d2b00", fontSize: 15 }}>{e.name}</div>
                      <div style={{ color: "#9a7d2e", fontSize: 13 }}>{e.role}</div>
                    </div>
                    <span style={{ background: statusColors[e.status] + "22", color: statusColors[e.status], borderRadius: 8, padding: "3px 12px", fontSize: 13, fontWeight: 600 }}>{e.status}</span>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {/* ORDERS */}
        {tab === "orders" && (
          <div>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 24, flexWrap: "wrap", gap: 12 }}>
              <div>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 28, fontWeight: 900, color: "#3d2b00" }}>📦 Orders</div>
                <div style={{ color: "#9a7d2e", fontSize: 14 }}>Tamam orders yahan manage karein</div>
              </div>
              <div style={{ display: "flex", gap: 10 }}>
                <input placeholder="Search orders..." value={search} onChange={e => setSearch(e.target.value)}
                  style={{ ...inputStyle, width: 200, marginBottom: 0 }} />
                <button style={btnPrimary} onClick={() => { setShowOrderForm(!showOrderForm); setEditOrderId(null); setOrderForm({ customer: "", item: "", amount: "", status: "Pending", date: "" }); }}>
                  + Naya Order
                </button>
              </div>
            </div>

            {showOrderForm && (
              <div style={{ background: "#fff", borderRadius: 16, border: "2px solid #e2c97e", padding: 24, marginBottom: 24, boxShadow: "0 4px 24px #c9a84c22" }}>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 18, color: "#3d2b00", marginBottom: 16, fontWeight: 700 }}>{editOrderId ? "Order Edit Karein" : "Naya Order Darj Karein"}</div>
                <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
                  <input placeholder="Customer ka naam" value={orderForm.customer} onChange={e => setOrderForm({ ...orderForm, customer: e.target.value })} style={inputStyle} />
                  <input placeholder="Item / Product" value={orderForm.item} onChange={e => setOrderForm({ ...orderForm, item: e.target.value })} style={inputStyle} />
                  <input placeholder="Amount (Rs.)" type="number" value={orderForm.amount} onChange={e => setOrderForm({ ...orderForm, amount: e.target.value })} style={inputStyle} />
                  <input type="date" value={orderForm.date} onChange={e => setOrderForm({ ...orderForm, date: e.target.value })} style={inputStyle} />
                  <select value={orderForm.status} onChange={e => setOrderForm({ ...orderForm, status: e.target.value })} style={{ ...inputStyle, gridColumn: "span 2" }}>
                    {["Pending", "Processing", "Delivered", "Cancelled"].map(s => <option key={s}>{s}</option>)}
                  </select>
                </div>
                <div style={{ display: "flex", gap: 10, marginTop: 4 }}>
                  <button style={btnPrimary} onClick={handleAddOrder}>{editOrderId ? "Update Karein" : "Save Karein"}</button>
                  <button style={btnGhost} onClick={() => { setShowOrderForm(false); setEditOrderId(null); }}>Raddkaren</button>
                </div>
              </div>
            )}

            <div style={{ background: "#fff", borderRadius: 16, border: "1.5px solid #e2c97e", overflow: "hidden", boxShadow: "0 2px 16px #c9a84c15" }}>
              <table style={{ width: "100%", borderCollapse: "collapse" }}>
                <thead>
                  <tr style={{ background: "linear-gradient(135deg, #3d2b00, #6b4c00)" }}>
                    {["Order ID", "Customer", "Item", "Amount", "Date", "Status", "Actions"].map(h => (
                      <th key={h} style={{ padding: "14px 16px", textAlign: "left", color: "#e8c96d", fontFamily: "Cormorant Garamond, serif", fontWeight: 700, fontSize: 14, letterSpacing: 0.5 }}>{h}</th>
                    ))}
                  </tr>
                </thead>
                <tbody>
                  {filteredOrders.length === 0 && (
                    <tr><td colSpan={7} style={{ textAlign: "center", padding: 32, color: "#9a7d2e" }}>Koi order nahi mila</td></tr>
                  )}
                  {filteredOrders.map((o, i) => (
                    <tr key={o.id} className="row-hover" style={{ background: i % 2 === 0 ? "#fffdf7" : "#fff", borderBottom: "1px solid #f5e6c0" }}>
                      <td style={{ padding: "12px 16px", color: "#c9a84c", fontWeight: 700, fontSize: 14 }}>{o.id}</td>
                      <td style={{ padding: "12px 16px", color: "#3d2b00", fontWeight: 600 }}>{o.customer}</td>
                      <td style={{ padding: "12px 16px", color: "#6b4c00" }}>{o.item}</td>
                      <td style={{ padding: "12px 16px", color: "#3d2b00", fontWeight: 600 }}>Rs. {Number(o.amount).toLocaleString()}</td>
                      <td style={{ padding: "12px 16px", color: "#9a7d2e", fontSize: 13 }}>{o.date}</td>
                      <td style={{ padding: "12px 16px" }}>
                        <span style={{ background: statusColors[o.status] + "22", color: statusColors[o.status], borderRadius: 8, padding: "4px 12px", fontSize: 13, fontWeight: 600 }}>{o.status}</span>
                      </td>
                      <td style={{ padding: "12px 16px" }}>
                        <button className="action-btn" onClick={() => startEditOrder(o)} style={{ background: "#3b82f611", color: "#3b82f6", border: "none", borderRadius: 7, padding: "5px 12px", cursor: "pointer", marginRight: 6, fontSize: 13, fontWeight: 600 }}>✏️ Edit</button>
                        <button className="action-btn" onClick={() => confirmDelete("order", o.id)} style={{ background: "#ef444411", color: "#ef4444", border: "none", borderRadius: 7, padding: "5px 12px", cursor: "pointer", fontSize: 13, fontWeight: 600 }}>🗑️</button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        )}

        {/* EMPLOYEES */}
        {tab === "employees" && (
          <div>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 24, flexWrap: "wrap", gap: 12 }}>
              <div>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 28, fontWeight: 900, color: "#3d2b00" }}>👥 Employees</div>
                <div style={{ color: "#9a7d2e", fontSize: 14 }}>Staff ki tamam details yahan manage karein</div>
              </div>
              <div style={{ display: "flex", gap: 10 }}>
                <input placeholder="Search employees..." value={search} onChange={e => setSearch(e.target.value)}
                  style={{ ...inputStyle, width: 200, marginBottom: 0 }} />
                <button style={btnPrimary} onClick={() => { setShowEmpForm(!showEmpForm); setEditEmpId(null); setEmpForm({ name: "", role: "", phone: "", salary: "", status: "Active" }); }}>
                  + Naya Employee
                </button>
              </div>
            </div>

            {showEmpForm && (
              <div style={{ background: "#fff", borderRadius: 16, border: "2px solid #e2c97e", padding: 24, marginBottom: 24, boxShadow: "0 4px 24px #c9a84c22" }}>
                <div style={{ fontFamily: "Playfair Display, serif", fontSize: 18, color: "#3d2b00", marginBottom: 16, fontWeight: 700 }}>{editEmpId ? "Employee Edit Karein" : "Naya Employee Darj Karein"}</div>
                <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
                  <input placeholder="Naam" value={empForm.name} onChange={e => setEmpForm({ ...empForm, name: e.target.value })} style={inputStyle} />
                  <input placeholder="Role / Designation" value={empForm.role} onChange={e => setEmpForm({ ...empForm, role: e.target.value })} style={inputStyle} />
                  <input placeholder="Phone Number" value={empForm.phone} onChange={e => setEmpForm({ ...empForm, phone: e.target.value })} style={inputStyle} />
                  <input placeholder="Monthly Salary (Rs.)" type="number" value={empForm.salary} onChange={e => setEmpForm({ ...empForm, salary: e.target.value })} style={inputStyle} />
                  <select value={empForm.status} onChange={e => setEmpForm({ ...empForm, status: e.target.value })} style={{ ...inputStyle, gridColumn: "span 2" }}>
                    {["Active", "On Leave", "Inactive"].map(s => <option key={s}>{s}</option>)}
                  </select>
                </div>
                <div style={{ display: "flex", gap: 10, marginTop: 4 }}>
                  <button sty