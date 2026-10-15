<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quản Lý Thu Chi Quỹ Lớp Theo Tháng (44 Thành Viên)</title>
<style>
  * { box-sizing: border-box; font-family: 'Segoe UI', Arial, sans-serif; margin: 0; padding: 0; }
  body { background: #f1f5f9; color: #0f172a; padding: 16px; line-height: 1.4; }
  .wrap { max-width: 1380px; margin: 0 auto; }
  .card { background: #fff; border-radius: 10px; padding: 16px 20px; margin-bottom: 14px; border: 1px solid #cbd5e1; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
  .top { display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; gap: 12px; }
  .btns { display: flex; flex-wrap: wrap; gap: 8px; }

  button { padding: 8px 14px; border-radius: 6px; border: 1px solid #cbd5e1; background: #fff; font-weight: 600; cursor: pointer; font-size: 13.5px; transition: 0.15s; }
  button:hover { background: #e2e8f0; }
  .btn-blue { background: #0284c7; color: #fff; border-color: #0284c7; }
  .btn-blue:hover { background: #0369a1; }
  .btn-green { background: #16a34a; color: #fff; border-color: #16a34a; }
  .btn-green:hover { background: #15803d; }
  .btn-red { background: #fee2e2; color: #dc2626; border-color: #fecaca; padding: 4px 9px; font-size: 12px; }
  .btn-red:hover { background: #fecaca; }
  .btn-xs { padding: 3px 7px; font-size: 11px; border-radius: 4px; }

  /* 4 Thẻ Tổng Quan Tự Động */
  .kpis { display: grid; grid-template-columns: repeat(auto-fit, minmax(230px, 1fr)); gap: 12px; margin-bottom: 14px; }
  .kpi { background: #fff; padding: 15px 18px; border-radius: 10px; border: 1px solid #cbd5e1; border-left: 5px solid #0284c7; }
  .kpi span { font-size: 12px; font-weight: 700; text-transform: uppercase; color: #64748b; display: block; }
  .kpi h2 { font-size: 25px; margin-top: 5px; font-weight: 700; }
  .kpi p { font-size: 12.5px; color: #64748b; margin-top: 5px; }

  /* Thanh chuyển Tab */
  .nav-tabs { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 14px; }
  .tab-item { padding: 10px 18px; border-radius: 8px; border: 1px solid #cbd5e1; background: #fff; font-weight: 700; font-size: 14px; cursor: pointer; color: #334155; }
  .tab-item.active { background: #0f172a; color: #fff; border-color: #0f172a; }

  /* Form nhập liệu */
  .form-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(155px, 1fr)); gap: 10px; align-items: end; margin-top: 10px; }
  .field label { display: block; font-size: 12.5px; font-weight: 600; margin-bottom: 4px; color: #334155; }
  .field input, .field select { width: 100%; padding: 8px 10px; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 14px; background: #fff; }
  .field input:focus, .field select:focus { border-color: #0284c7; outline: none; }

  /* Bảng dữ liệu */
  .table-wrap { overflow-x: auto; max-height: 68vh; border: 1px solid #cbd5e1; border-radius: 8px; background: #fff; }
  table { width: 100%; border-collapse: collapse; font-size: 13.5px; text-align: center; }
  th { position: sticky; top: 0; background: #1e293b; color: #fff; padding: 10px 8px; border: 1px solid #334155; z-index: 10; white-space: nowrap; }
  td { padding: 7px 8px; border: 1px solid #e2e8f0; vertical-align: middle; }
  tr:hover td { background: #f0f9ff; }
  tfoot td { position: sticky; bottom: 0; background: #f1f5f9; font-weight: 700; padding: 10px 8px; border-top: 2px solid #94a3b8; z-index: 9; }

  .name-inp { width: 100%; min-width: 185px; padding: 5px 7px; border: 1px solid #cbd5e1; border-radius: 4px; font-size: 13.5px; }
  .fee-inp { width: 95px; padding: 4px 6px; text-align: center; font-weight: 700; border-radius: 4px; border: 1px solid #94a3b8; background: #fef9c3; color: #854d0e; font-size: 13px; }
  .month-inp { width: 105px; padding: 3px 6px; text-align: center; font-weight: 700; border-radius: 4px; border: 1px solid #475569; background: #fff; color: #0f172a; margin-bottom: 4px; }
  input[type="checkbox"] { width: 19px; height: 19px; cursor: pointer; accent-color: #16a34a; }

  .badge { display: inline-block; padding: 3px 8px; border-radius: 99px; font-size: 12px; font-weight: 700; }
  .b-green { background: #dcfce7; color: #15803d; }
  .b-amber { background: #fef3c7; color: #b45309; }
  .b-blue { background: #e0f2fe; color: #0369a1; }

  #bulkBox { display: none; margin-top: 12px; padding-top: 12px; border-top: 1px dashed #cbd5e1; }
  textarea { width: 100%; height: 130px; padding: 8px; margin: 8px 0; border: 1px solid #94a3b8; border-radius: 6px; }
</style>
</head>
<body>

<div class="wrap">
  <!-- Header -->
  <div class="card">
    <div class="top">
      <div>
        <h2>📒 Hệ Thống Quản Lý Thu - Chi Quỹ Lớp Theo Tháng (44 Thành Viên)</h2>
        <p style="font-size:13px; color:#64748b; margin-top:4px;">Tích tên đến đâu tự động nhân tiền quỹ từng tháng đến đó • Tự động trừ khi ghi khoản chi</p>
      </div>
      <div class="btns">
        <button type="button" onclick="toggleBulk()">📝 Dán nhanh 44 tên</button>
        <button type="button" class="btn-blue" onclick="addMonth()">➕ Thêm tháng thu quỹ</button>
        <button type="button" class="btn-green" onclick="exportAllCSV()">📥 Xuất báo cáo Excel (CSV)</button>
      </div>
    </div>

    <div id="bulkBox">
      <p style="font-size:13px; font-weight:600;">Dán danh sách 44 học sinh (mỗi tên 1 dòng) vào đây rồi bấm "Cập nhật":</p>
      <textarea id="bulkInput" placeholder="Nguyễn Văn A&#10;Trần Thị B..."></textarea>
      <button type="button" class="btn-blue" onclick="applyBulkNames()">✓ Cập nhật danh sách 44 tên</button>
      <button type="button" onclick="toggleBulk()">Đóng</button>
    </div>
  </div>

  <!-- 4 Thẻ Tổng Quan Tự Động Nhảy Số -->
  <div class="kpis">
    <div class="kpi" style="border-left-color:#2563eb;">
      <span>💰 Tổng Quỹ Thu Được (Tất cả tháng)</span>
      <h2 id="kpiTotalIn" style="color:#2563eb;">0 đ</h2>
      <p id="kpiSubIn">Từ đóng quỹ 44 người & thu khác</p>
    </div>
    <div class="kpi" style="border-left-color:#dc2626;">
      <span>💸 Tổng Tiền Đã Chi</span>
      <h2 id="kpiTotalOut" style="color:#dc2626;">0 đ</h2>
      <p id="kpiSubOut">0 khoản chi đã ghi</p>
    </div>
    <div class="kpi" style="border-left-color:#16a34a;">
      <span>🏦 Số Dư Quỹ Hiện Tại (Thu - Chi)</span>
      <h2 id="kpiBalance" style="color:#16a34a;">0 đ</h2>
      <p id="kpiSubBal">Tự động cập nhật tức thì</p>
    </div>
    <div class="kpi" style="border-left-color:#d97706;">
      <span>📊 Tiến Độ Đóng Quỹ Các Tháng</span>
      <h2 id="kpiPaidRate" style="color:#d97706;">0 lượt</h2>
      <p id="kpiSubRate">Nhấn vào từng ô để đánh dấu đã nộp</p>
    </div>
  </div>

  <!-- Bảng Tổng Hợp Nhanh Thu - Chi Từng Tháng (Luôn hiển thị để theo dõi) -->
  <div class="card">
    <h3 style="font-size:15px; margin-bottom:10px;">📊 Bảng Thống Kê Quỹ Từng Tháng (Tự động tính 100%)</h3>
    <div class="table-wrap" style="max-height:260px;">
      <table>
        <thead>
          <tr>
            <th>Tháng</th>
            <th>Mức đóng / 1 người (Sửa trực tiếp)</th>
            <th>Số người đã đóng</th>
            <th>Tiền thu từ 44 người</th>
            <th>Thu thêm / Quỹ tồn</th>
            <th>TỔNG THU THÁNG</th>
            <th>TỔNG CHI THÁNG</th>
            <th>CÒN DƯ TRONG THÁNG</th>
          </tr>
        </thead>
        <tbody id="monthSummaryBody"></tbody>
        <tfoot>
          <tr id="monthSummaryFoot"></tr>
        </tfoot>
      </table>
    </div>
  </div>

  <!-- Các nút chuyển chế độ làm việc -->
  <div class="nav-tabs">
    <button type="button" class="tab-item active" id="tabBtn1" onclick="switchTab(1)">1️⃣ Bảng Tích Đóng Quỹ 44 Người (Theo Tháng)</button>
    <button type="button" class="tab-item" id="tabBtn2" onclick="switchTab(2)">2️⃣ Ghi Các Khoản Chi & Thu Thêm Ngoài Quỹ</button>
  </div>

  <!-- TAB 1: BẢNG ĐÓNG QUỸ 44 NGƯỜI THEO THÁNG -->
  <div id="tabContent1" class="card">
    <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px; margin-bottom:10px;">
      <p style="font-size:13.5px; color:#334155;">
        💡 <b>Hướng dẫn:</b> Bạn có thể sửa <b>Mức tiền/người</b> ở ô màu vàng trên đầu mỗi tháng. Tích vào ô vuông của ai là tiền tháng đó tự động cộng thêm!
      </p>
      <input type="text" id="searchStudent" placeholder="🔍 Tìm tên học sinh hoặc STT..." oninput="renderStudentTable()" style="padding:7px 12px; border:1px solid #cbd5e1; border-radius:6px; min-width:230px;">
    </div>

    <div class="table-wrap">
      <table>
        <thead><tr id="stuHead"></tr></thead>
        <tbody id="stuBody"></tbody>
        <tfoot><tr id="stuFoot"></tr></tfoot>
      </table>
    </div>
  </div>

  <!-- TAB 2: GHI KHOẢN CHI & THU THÊM -->
  <div id="tabContent2" style="display:none;">
    <!-- Khung ghi khoản chi -->
    <div class="card">
      <h3 style="font-size:15.5px; color:#dc2626;">➖ Ghi Khoản Chi Mới Của Lớp (Tự động trừ vào quỹ)</h3>
      <div class="form-row">
        <div class="field">
          <label>Thuộc tháng</label>
          <select id="exMonth"></select>
        </div>
        <div class="field">
          <label>Ngày chi</label>
          <input type="date" id="exDate">
        </div>
        <div class="field" style="grid-column: span 2;">
          <label>Nội dung khoản chi *</label>
          <input type="text" id="exTitle" placeholder="VD: Photo đề cương Toán, Mua nước giải khát...">
        </div>
        <div class="field">
          <label>Danh mục</label>
          <select id="exCat">
            <option value="Học tập / Photo">📚 Học tập / Photo</option>
            <option value="Phong trào / Đoàn">🚩 Phong trào / Đoàn</option>
            <option value="Liên hoan / Ăn uống">🍕 Liên hoan / Ăn uống</option>
            <option value="Vệ sinh / Trang trí">🧹 Vệ sinh / Trang trí</option>
            <option value="Quà tặng / Khác">🎁 Quà tặng / Khác</option>
          </select>
        </div>
        <div class="field">
          <label>Số tiền chi (VNĐ) *</label>
          <input type="text" id="exAmount" placeholder="VD: 150000 hoặc 150.000">
        </div>
        <div class="field">
          <label>Người chi / Ứng</label>
          <input type="text" id="exPayer" placeholder="VD: Thủ quỹ">
        </div>
        <div class="field">
          <button type="button" class="btn-blue" style="width:100%; background:#dc2626; border-color:#dc2626;" onclick="addExpense()">➕ Lưu khoản chi</button>
        </div>
      </div>
    </div>

    <!-- Khung ghi khoản thu ngoài (nếu có) -->
    <div class="card">
      <h3 style="font-size:15.5px; color:#16a34a;">➕ Cộng Thêm Khoản Thu Ngoài / Quỹ Tồn Cũ (Không phải tiền đóng từng người)</h3>
      <div class="form-row">
        <div class="field">
          <label>Cộng vào tháng</label>
          <select id="inMonth"></select>
        </div>
        <div class="field" style="grid-column: span 2;">
          <label>Nội dung khoản thu thêm *</label>
          <input type="text" id="inTitle" placeholder="VD: Quỹ cũ bàn giao, Tiền thưởng văn nghệ, Bán giấy vụn...">
        </div>
        <div class="field">
          <label>Số tiền thu thêm (VNĐ) *</label>
          <input type="text" id="inAmount" placeholder="VD: 500000 hoặc 500.000">
        </div>
        <div class="field">
          <button type="button" class="btn-green" style="width:100%;" onclick="addExtraIncome()">➕ Cộng vào quỹ</button>
        </div>
      </div>
      <div id="extraIncomeList" style="margin-top:10px; font-size:13px; color:#334155;"></div>
    </div>

    <!-- Bảng lịch sử các khoản chi -->
    <div class="card">
      <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px; margin-bottom:10px;">
        <h3 style="font-size:15.5px;">📋 Danh Sách Chi Tiết Các Khoản Đã Chi</h3>
        <div style="display:flex; gap:8px; align-items:center;">
          <select id="filterExMonth" onchange="renderExpenses()" style="padding:6px 10px; border:1px solid #cbd5e1; border-radius:6px;">
            <option value="ALL">Tất cả các tháng</option>
          </select>
          <input type="text" id="searchEx" placeholder="🔍 Tìm khoản chi..." oninput="renderExpenses()" style="padding:6px 12px; border:1px solid #cbd5e1; border-radius:6px;">
        </div>
      </div>

      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th style="width:50px;">STT</th>
              <th>Tháng</th>
              <th>Ngày</th>
              <th style="text-align:left;">Nội dung khoản chi</th>
              <th>Danh mục</th>
              <th>Người chi</th>
              <th>Trạng thái (Nhấn để đổi)</th>
              <th style="text-align:right;">Số tiền chi</th>
              <th style="width:70px;">Xóa</th>
            </tr>
          </thead>
          <tbody id="exBody"></tbody>
          <tfoot>
            <tr>
              <td colspan="7" style="text-align:right;">TỔNG TIỀN CHI ĐANG HIỂN THỊ:</td>
              <td id="exFootSum" style="text-align:right; color:#dc2626;">0 đ</td>
              <td></td>
            </tr>
          </tfoot>
        </table>
      </div>
    </div>
  </div>
</div>

<script>
  var N = 44;
  var STORAGE_KEY = 'quy_lop_44_theo_thang_v2';

  var state = {
    months: [
      { id: 'm1', name: 'Tháng 9', fee: 50000 },
      { id: 'm2', name: 'Tháng 10', fee: 50000 },
      { id: 'm3', name: 'Tháng 11', fee: 50000 },
      { id: 'm4', name: 'Tháng 12', fee: 50000 }
    ],
    students: [],
    expenses: [],
    extraIncomes: []
  };

  for (var i = 0; i < N; i++) {
    state.students.push({
      id: i + 1,
      name: '',
      paid: { m1: false, m2: false, m3: false, m4: false }
    });
  }

  document.getElementById('exDate').value = new Date().toISOString().slice(0, 10);

  // Hàm đọc số tiền thông minh: chấp nhận cả "50000", "50.000", "50,000"
  function parseMoney(val) {
    if (typeof val === 'number') return val;
    var clean = String(val || '').replace(/[^0-9]/g, '');
    return parseInt(clean, 10) || 0;
  }

  function fmtMoney(num) {
    return (Number(num) || 0).toLocaleString('vi-VN') + ' đ';
  }

  function esc(str) {
    return String(str || '').replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
  }

  function loadData() {
    try {
      var raw = localStorage.getItem(STORAGE_KEY);
      if (raw) {
        var parsed = JSON.parse(raw);
        if (parsed && parsed.students && parsed.students.length === N && parsed.months) {
          state = parsed;
          if (!state.extraIncomes) state.extraIncomes = [];
          if (!state.expenses) state.expenses = [];
        }
      }
    } catch (e) {}
  }

  function saveData() {
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    } catch (e) {}
    refreshAll();
  }

  function switchTab(tabNum) {
    document.getElementById('tabContent1').style.display = tabNum === 1 ? 'block' : 'none';
    document.getElementById('tabContent2').style.display = tabNum === 2 ? 'block' : 'none';
    document.getElementById('tabBtn1').className = 'tab-item ' + (tabNum === 1 ? 'active' : '');
    document.getElementById('tabBtn2').className = 'tab-item ' + (tabNum === 2 ? 'active' : '');
  }

  // Tính toán thống kê từng tháng và toàn bộ quỹ
  function refreshAll() {
    updateMonthSelects();
    renderMonthSummary();
    renderStudentTable();
    renderExpenses();
    renderExtraIncomes();
  }

  function updateMonthSelects() {
    var exSel = document.getElementById('exMonth');
    var inSel = document.getElementById('inMonth');
    var filSel = document.getElementById('filterExMonth');

    var curEx = exSel.value;
    var curIn = inSel.value;
    var curFil = filSel.value || 'ALL';

    var opts = '';
    for (var i = 0; i < state.months.length; i++) {
      var m = state.months[i];
      opts += '<option value="' + m.id + '">' + esc(m.name) + '</option>';
    }
    exSel.innerHTML = opts;
    inSel.innerHTML = opts;
    filSel.innerHTML = '<option value="ALL">Tất cả các tháng</option>' + opts;

    if (curEx) exSel.value = curEx;
    if (curIn) inSel.value = curIn;
    filSel.value = curFil;
  }

  function renderMonthSummary() {
    var totalInAll = 0;
    var totalOutAll = 0;
    var totalPaidChecks = 0;
    var totalStudentFundAll = 0;
    var totalExtraAll = 0;

    var rowsHtml = '';

    for (var i = 0; i < state.months.length; i++) {
      var m = state.months[i];
      var paidCount = 0;
      for (var s = 0; s < N; s++) {
        if (state.students[s].paid[m.id]) paidCount++;
      }
      totalPaidChecks += paidCount;

      var studentFund = paidCount * (Number(m.fee) || 0);
      totalStudentFundAll += studentFund;

      var extraIn = 0;
      for (var e = 0; e < state.extraIncomes.length; e++) {
        if (state.extraIncomes[e].monthId === m.id) {
          extraIn += Number(state.extraIncomes[e].amount) || 0;
        }
      }
      totalExtraAll += extraIn;

      var monthOut = 0;
      for (var x = 0; x < state.expenses.length; x++) {
        if (state.expenses[x].monthId === m.id) {
          monthOut += Number(state.expenses[x].amount) || 0;
        }
      }

      var monthTotalIn = studentFund + extraIn;
      var monthRemain = monthTotalIn - monthOut;

      totalInAll += monthTotalIn;
      totalOutAll += monthOut;

      rowsHtml += '<tr>' +
        '<td><b>' + esc(m.name) + '</b></td>' +
        '<td><input type="text" class="fee-inp" value="' + (Number(m.fee) || 0).toLocaleString('vi-VN') + '" onchange="updateMonthFee(' + i + ', this.value)" title="Sửa mức tiền đóng 1 người của tháng này"> đ</td>' +
        '<td><span class="badge b-blue">' + paidCount + ' / 44 người</span></td>' +
        '<td style="font-weight:600; color:#0284c7;">+' + fmtMoney(studentFund) + '</td>' +
        '<td style="color:#0369a1;">+' + fmtMoney(extraIn) + '</td>' +
        '<td style="font-weight:700; color:#2563eb;">' + fmtMoney(monthTotalIn) + '</td>' +
        '<td style="font-weight:700; color:#dc2626;">-' + fmtMoney(monthOut) + '</td>' +
        '<td style="font-weight:700; color:' + (monthRemain >= 0 ? '#16a34a' : '#dc2626') + ';">' + fmtMoney(monthRemain) + '</td>' +
        '</tr>';
    }

    document.getElementById('monthSummaryBody').innerHTML = rowsHtml;

    var netBalance = totalInAll - totalOutAll;
    document.getElementById('monthSummaryFoot').innerHTML =
      '<td colspan="2" style="text-align:right;">TỔNG CỘNG CÁC THÁNG:</td>' +
      '<td>' + totalPaidChecks + ' lượt đóng</td>' +
      '<td style="color:#0284c7;">+' + fmtMoney(totalStudentFundAll) + '</td>' +
      '<td style="color:#0369a1;">+' + fmtMoney(totalExtraAll) + '</td>' +
      '<td style="color:#2563eb;">' + fmtMoney(totalInAll) + '</td>' +
      '<td style="color:#dc2626;">-' + fmtMoney(totalOutAll) + '</td>' +
      '<td style="color:' + (netBalance >= 0 ? '#16a34a' : '#dc2626') + ';">' + fmtMoney(netBalance) + '</td>';

    // Cập nhật 4 thẻ KPI trên đầu
    document.getElementById('kpiTotalIn').textContent = fmtMoney(totalInAll);
    document.getElementById('kpiSubIn').textContent = 'Đóng quỹ: ' + fmtMoney(totalStudentFundAll) + ' | Thu thêm: ' + fmtMoney(totalExtraAll);
    document.getElementById('kpiTotalOut').textContent = fmtMoney(totalOutAll);
    document.getElementById('kpiSubOut').textContent = state.expenses.length + ' khoản chi đã ghi';
    document.getElementById('kpiBalance').textContent = fmtMoney(netBalance);
    document.getElementById('kpiBalance').style.color = netBalance >= 0 ? '#16a34a' : '#dc2626';
    document.getElementById('kpiPaidRate').textContent = totalPaidChecks + ' / ' + (N * state.months.length) + ' lượt';
  }

  function renderStudentTable() {
    var h = '<th style="width:48px;">STT</th><th style="min-width:200px; text-align:left;">Họ và Tên (44 Thành Viên)</th>';
    for (var i = 0; i < state.months.length; i++) {
      var m = state.months[i];
      var delBtn = state.months.length > 1
        ? '<button type="button" class="btn-red btn-xs" onclick="deleteMonth(' + i + ')" title="Xóa tháng này">✕</button>'
        : '';
      h += '<th>' +
        '<div><input type="text" class="month-inp" value="' + esc(m.name) + '" onchange="renameMonth(' + i + ', this.value)"> ' + delBtn + '</div>' +
        '<div style="font-size:11.5px; color:#fde047; margin-bottom:5px;">Mức: ' + fmtMoney(m.fee) + '/người</div>' +
        '<div style="display:flex; gap:4px; justify-content:center;">' +
          '<button type="button" class="btn-xs" style="background:#dcfce7; color:#15803d; border:none;" onclick="markAllMonth(\'' + m.id + '\', true)">✓ Cả lớp</button>' +
          '<button type="button" class="btn-xs" style="background:#f1f5f9; color:#475569; border:none;" onclick="markAllMonth(\'' + m.id + '\', false)">Bỏ tích</button>' +
        '</div>' +
      '</th>';
    }
    h += '<th>Số tháng đã đóng</th><th>Tổng tiền đã nộp</th>';
    document.getElementById('stuHead').innerHTML = h;

    var q = (document.getElementById('searchStudent').value || '').toLowerCase().trim();
    var b = '';

    for (var s = 0; s < N; s++) {
      var st = state.students[s];
      if (q && st.name.toLowerCase().indexOf(q) === -1 && String(st.id).indexOf(q) === -1) continue;

      var mCount = 0;
      var mMoney = 0;
      var checkCells = '';

      for (var i = 0; i < state.months.length; i++) {
        var m = state.months[i];
        var isPaid = !!st.paid[m.id];
        if (isPaid) {
          mCount++;
          mMoney += Number(m.fee) || 0;
        }
        checkCells += '<td style="background:' + (isPaid ? '#f0fdf4' : '#fff') + ';">' +
          '<input type="checkbox" ' + (isPaid ? 'checked' : '') + ' onchange="toggleStudentPaid(' + s + ', \'' + m.id + '\', this.checked)">' +
        '</td>';
      }

      b += '<tr>' +
        '<td><b>' + st.id + '</b></td>' +
        '<td style="text-align:left;"><input type="text" class="name-inp" placeholder="Nhập tên thành viên ' + st.id + '..." value="' + esc(st.name) + '" oninput="updateStudentName(' + s + ', this.value)"></td>' +
        checkCells +
        '<td><span class="badge ' + (mCount === state.months.length ? 'b-green' : 'b-amber') + '">' + mCount + ' / ' + state.months.length + ' tháng</span></td>' +
        '<td style="font-weight:700; color:#15803d;">' + fmtMoney(mMoney) + '</td>' +
      '</tr>';
    }
    document.getElementById('stuBody').innerHTML = b;

    // Dòng tổng thu từng cột tháng ngay dưới bảng 44 người
    var f = '<td colspan="2" style="text-align:right;">THU ĐƯỢC TỪNG THÁNG:</td>';
    var grandStudentMoney = 0;
    for (var i = 0; i < state.months.length; i++) {
      var m = state.months[i];
      var cnt = 0;
      for (var s = 0; s < N; s++) if (state.students[s].paid[m.id]) cnt++;
      var sumM = cnt * (Number(m.fee) || 0);
      grandStudentMoney += sumM;
      f += '<td style="color:#15803d;">' + fmtMoney(sumM) + '<br><small style="color:#64748b;">(' + cnt + '/44 người)</small></td>';
    }
    f += '<td colspan="2" style="color:#2563eb; font-size:15px;">Tổng: ' + fmtMoney(grandStudentMoney) + '</td>';
    document.getElementById('stuFoot').innerHTML = f;
  }

  function updateStudentName(sIdx, val) {
    state.students[sIdx].name = val;
    try { localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); } catch (e) {}
  }

  function toggleStudentPaid(sIdx, monthId, checked) {
    state.students[sIdx].paid[monthId] = checked;
    saveData();
  }

  function markAllMonth(monthId, status) {
    for (var s = 0; s < N; s++) {
      state.students[s].paid[monthId] = status;
    }
    saveData();
  }

  function updateMonthFee(mIdx, val) {
    state.months[mIdx].fee = parseMoney(val);
    saveData();
  }

  function renameMonth(mIdx, val) {
    state.months[mIdx].name = (val || '').trim() || ('Tháng ' + (mIdx + 1));
    saveData();
  }

  function addMonth() {
    var defaultFee = state.months.length > 0 ? state.months[state.months.length - 1].fee : 50000;
    var newId = 'm_' + Date.now();
    var newName = 'Tháng mới ' + (state.months.length + 1);
    state.months.push({ id: newId, name: newName, fee: defaultFee });
    for (var s = 0; s < N; s++) {
      state.students[s].paid[newId] = false;
    }
    saveData();
  }

  function deleteMonth(mIdx) {
    if (state.months.length <= 1) return;
    var m = state.months[mIdx];
    if (!confirm('Xóa "' + m.name + '" khỏi bảng thu quỹ?')) return;
    state.months.splice(mIdx, 1);
    saveData();
  }

  function addExpense() {
    var monthId = document.getElementById('exMonth').value;
    var date = document.getElementById('exDate').value;
    var title = document.getElementById('exTitle').value.trim();
    var cat = document.getElementById('exCat').value;
    var amount = parseMoney(document.getElementById('exAmount').value);
    var payer = document.getElementById('exPayer').value.trim() || 'Thủ quỹ';

    if (!title) {
      alert('Vui lòng nhập nội dung khoản chi!');
      return;
    }
    if (amount <= 0) {
      alert('Vui lòng nhập số tiền chi lớn hơn 0!');
      return;
    }

    state.expenses.unshift({
      id: Date.now(),
      monthId: monthId,
      date: date,
      title: title,
      category: cat,
      amount: amount,
      payer: payer,
      status: 'paid'
    });

    document.getElementById('exTitle').value = '';
    document.getElementById('exAmount').value = '';
    saveData();
  }

  function addExtraIncome() {
    var monthId = document.getElementById('inMonth').value;
    var title = document.getElementById('inTitle').value.trim();
    var amount = parseMoney(document.getElementById('inAmount').value);

    if (!title || amount <= 0) {
      alert('Vui lòng nhập tên khoản thu thêm và số tiền hợp lệ!');
      return;
    }

    state.extraIncomes.push({
      id: Date.now(),
      monthId: monthId,
      title: title,
      amount: amount
    });

    document.getElementById('inTitle').value = '';
    document.getElementById('inAmount').value = '';
    saveData();
  }

  function removeExtraIncome(idx) {
    state.extraIncomes.splice(idx, 1);
    saveData();
  }

  function renderExtraIncomes() {
    var el = document.getElementById('extraIncomeList');
    if (!state.extraIncomes.length) {
      el.innerHTML = '<i>Chưa có khoản thu ngoài nào (Tiền đóng của 44 thành viên đã được tính tự động ở Tab 1).</i>';
      return;
    }
    var html = '<b>Các khoản thu ngoài đã cộng:</b> ';
    for (var i = 0; i < state.extraIncomes.length; i++) {
      var item = state.extraIncomes[i];
      var mName = getMonthName(item.monthId);
      html += '<span class="badge b-green" style="margin:3px;">[' + esc(mName) + '] ' + esc(item.title) + ': +' + fmtMoney(item.amount) +
        ' <b style="cursor:pointer;color:#dc2626;margin-left:4px;" onclick="removeExtraIncome(' + i + ')">✕</b></span>';
    }
    el.innerHTML = html;
  }

  function getMonthName(monthId) {
    for (var i = 0; i < state.months.length; i++) {
      if (state.months[i].id === monthId) return state.months[i].name;
    }
    return 'Khác';
  }

  function toggleExStatus(idx) {
    var ex = state.expenses[idx];
    if (!ex) return;
    ex.status = ex.status === 'paid' ? 'pending' : 'paid';
    saveData();
  }

  function deleteExpense(idx) {
    if (!confirm('Xóa khoản chi này?')) return;
    state.expenses.splice(idx, 1);
    saveData();
  }

  function renderExpenses() {
    var fMonth = document.getElementById('filterExMonth').value;
    var q = (document.getElementById('searchEx').value || '').toLowerCase().trim();
    var html = '';
    var sum = 0;
    var stt = 1;

    for (var i = 0; i < state.expenses.length; i++) {
      var ex = state.expenses[i];
      if (fMonth !== 'ALL' && ex.monthId !== fMonth) continue;
      if (q && ex.title.toLowerCase().indexOf(q) === -1 && ex.payer.toLowerCase().indexOf(q) === -1) continue;

      sum += Number(ex.amount) || 0;
      var stBadge = ex.status === 'paid'
        ? '<span class="badge b-green" style="cursor:pointer;" onclick="toggleExStatus(' + i + ')">✓ Đã xuất quỹ</span>'
        : '<span class="badge b-amber" style="cursor:pointer;" onclick="toggleExStatus(' + i + ')">⏳ Cần hoàn tiền</span>';

      html += '<tr>' +
        '<td>' + (stt++) + '</td>' +
        '<td><span class="badge b-blue">' + esc(getMonthName(ex.monthId)) + '</span></td>' +
        '<td>' + esc(ex.date) + '</td>' +
        '<td style="text-align:left;"><b>' + esc(ex.title) + '</b></td>' +
        '<td>' + esc(ex.category) + '</td>' +
        '<td>' + esc(ex.payer) + '</td>' +
        '<td>' + stBadge + '</td>' +
        '<td style="text-align:right; font-weight:700; color:#dc2626;">-' + fmtMoney(ex.amount) + '</td>' +
        '<td><button type="button" class="btn-red" onclick="deleteExpense(' + i + ')">Xóa</button></td>' +
      '</tr>';
    }

    if (!html) {
      html = '<tr><td colspan="9" style="padding:20px; color:#64748b;">Chưa có khoản chi nào trong mục này.</td></tr>';
    }

    document.getElementById('exBody').innerHTML = html;
    document.getElementById('exFootSum').textContent = '-' + fmtMoney(sum);
  }

  function toggleBulk() {
    var box = document.getElementById('bulkBox');
    if (box.style.display === 'block') {
      box.style.display = 'none';
    } else {
      var names = [];
      for (var i = 0; i < N; i++) names.push(state.students[i].name);
      document.getElementById('bulkInput').value = names.join('\n').trim();
      box.style.display = 'block';
    }
  }

  function applyBulkNames() {
    var lines = document.getElementById('bulkInput').value.split(/\r?\n/);
    for (var i = 0; i < N; i++) {
      if (lines[i] !== undefined) state.students[i].name = lines[i].trim();
    }
    saveData();
    document.getElementById('bulkBox').style.display = 'none';
  }

  function exportAllCSV() {
    var csv = '\uFEFF--- BẢNG 1: TỔNG HỢP THU CHI TỪNG THÁNG ---\n';
    csv += 'Tháng,Mức đóng/người,Số người đã đóng,Tiền thu 44 người,Thu thêm ngoài,Tổng Thu Tháng,Tổng Chi Tháng,Còn Dư Tháng\n';

    for (var i = 0; i < state.months.length; i++) {
      var m = state.months[i];
      var cnt = 0;
      for (var s = 0; s < N; s++) if (state.students[s].paid[m.id]) cnt++;
      var sFund = cnt * (Number(m.fee) || 0);
      var exIn = 0;
      for (var e = 0; e < state.extraIncomes.length; e++) if (state.extraIncomes[e].monthId === m.id) exIn += Number(state.extraIncomes[e].amount) || 0;
      var mOut = 0;
      for (var x = 0; x < state.expenses.length; x++) if (state.expenses[x].monthId === m.id) mOut += Number(state.expenses[x].amount) || 0;

      csv += ['"' + m.name + '"', m.fee, cnt + '/44', sFund, exIn, sFund + exIn, mOut, (sFund + exIn - mOut)].join(',') + '\n';
    }

    csv += '\n--- BẢNG 2: DANH SÁCH ĐÓNG QUỸ 44 THÀNH VIÊN ---\n';
    var mHeaders = ['STT', 'Họ và Tên'];
    for (var i = 0; i < state.months.length; i++) mHeaders.push('"' + state.months[i].name + '"');
    mHeaders.push('Tổng tiền đã đóng');
    csv += mHeaders.join(',') + '\n';

    for (var s = 0; s < N; s++) {
      var st = state.students[s];
      var row = [st.id, '"' + (st.name || ('Thành viên ' + st.id)).replace(/"/g, '""') + '"'];
      var sumSt = 0;
      for (var i = 0; i < state.months.length; i++) {
        var m = state.months[i];
        var ok = !!st.paid[m.id];
        if (ok) sumSt += Number(m.fee) || 0;
        row.push(ok ? m.fee : 0);
      }
      row.push(sumSt);
      csv += row.join(',') + '\n';
    }

    csv += '\n--- BẢNG 3: CHI TIẾT CÁC KHOẢN CHI ---\n';
    csv += 'STT,Tháng,Ngày,Nội dung chi,Danh mục,Người chi,Số tiền\n';
    for (var x = 0; x < state.expenses.length; x++) {
      var ex = state.expenses[x];
      csv += [x + 1, '"' + getMonthName(ex.monthId) + '"', ex.date, '"' + ex.title.replace(/"/g, '""') + '"', '"' + ex.category + '"', '"' + ex.payer + '"', ex.amount].join(',') + '\n';
    }

    var a = document.createElement('a');
    a.href = URL.createObjectURL(new Blob([csv], { type: 'text/csv;charset=utf-8;' }));
    a.download = 'bao-cao-thu-chi-quy-lop-theo-thang.csv';
    a.click();
  }

  loadData();
  refreshAll();
</script>
</body>
</html>
