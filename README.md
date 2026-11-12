<!doctype html><html lang="fa" dir="rtl"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>مدیریت کالاهای تعمیری</title>
<style>
*{box-sizing:border-box}body{margin:0;background:#f5f6fa;color:#222;font-family:Tahoma,Arial,sans-serif}
header{background:linear-gradient(135deg,#5b21b6,#7c3aed);color:white;padding:24px}.wrap,main{max-width:1500px;margin:auto}
.top{display:flex;justify-content:space-between;gap:15px}.logo{font-size:23px;font-weight:bold}.search{position:relative;margin-top:20px}
.search input{width:100%;padding:15px 45px 15px 15px;border:0;border-radius:13px;font-size:15px}.search span{position:absolute;right:15px;top:12px;font-size:22px}
main{padding:25px 15px}.buttons{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:22px}button{font:inherit;border:0;border-radius:11px;padding:12px 17px;cursor:pointer;font-weight:bold}
.add,.active{background:#6d28d9;color:white}.tab{background:white;box-shadow:0 2px 10px #0001}
.table-wrap{background:white;border-radius:17px;box-shadow:0 4px 18px #0001;overflow:auto;max-height:calc(100vh - 250px)}
table{width:100%;min-width:1250px;border-collapse:collapse;direction:rtl}th,td{padding:14px 12px;border-bottom:1px solid #eee;text-align:right;vertical-align:top}
th{position:sticky;top:0;background:#faf9ff;color:#5b21b6;z-index:1;white-space:nowrap}td{line-height:1.8;white-space:pre-wrap;overflow-wrap:anywhere}
.code{display:inline-block;padding:6px 10px;border-radius:8px;background:#eee7ff;color:#5b21b6;font-weight:bold}.status{display:inline-block;padding:6px 10px;border-radius:8px;font-size:12px;white-space:nowrap}
.repairing{background:#fff1cf;color:#a16207}.repaired{background:#dcfce7;color:#15803d}.price{color:#15803d;font-weight:bold}.muted{color:#777}
.actions{display:flex;gap:8px;flex-wrap:wrap}.repair{background:#16a34a;color:#fff}.edit{background:#ede9fe;color:#5b21b6}.del{background:#fee2e2;color:#b91c1c}
.empty{background:white;border-radius:17px;padding:45px;text-align:center;color:#777}.modal{display:none;position:fixed;inset:0;background:#0008;align-items:center;justify-content:center;padding:18px;z-index:10}
.modal.show{display:flex}.box{background:white;width:100%;max-width:600px;max-height:92vh;overflow:auto;border-radius:18px;padding:23px}
.group{margin:14px 0}.group label{display:block;font-weight:bold;margin-bottom:7px}.group input,.group textarea{width:100%;padding:13px;border:1px solid #ddd;border-radius:10px;font:inherit}
.group input{min-height:52px}.group textarea{min-height:220px;resize:vertical;overflow:auto}.hint{display:block;color:#777;font-size:12px;margin-top:6px}
.modal-actions{display:flex;gap:10px;margin-top:18px}.save{background:#6d28d9;color:#fff;flex:1}.cancel{background:#eee;flex:1}.required{color:#b91c1c}.price-words{margin-top:10px;color:#15803d;font-weight:bold;min-height:24px}

.support-float{position:fixed;right:18px;bottom:18px;z-index:20}
.support-btn{width:48px;height:48px;border-radius:50%;background:#6d28d9;color:#fff;display:flex;align-items:center;justify-content:center;font-size:23px;box-shadow:0 5px 18px #0003;cursor:pointer;border:0}
.support-box{display:none;position:absolute;right:0;bottom:58px;width:285px;background:#fff;border-radius:16px;padding:16px;box-shadow:0 6px 25px #0003;border:1px solid #eee;line-height:1.9}
.support-box.show{display:block}.support-box b{color:#5b21b6}.support-box a{color:#6d28d9;font-weight:bold;text-decoration:none}

.autocomplete-wrap{position:relative}
.autocomplete-list{display:none;position:absolute;top:100%;left:0;right:0;background:#fff;border:1px solid #ddd;border-top:0;border-radius:0 0 10px 10px;box-shadow:0 5px 14px #0002;z-index:30;max-height:190px;overflow:auto}
.autocomplete-list.show{display:block}
.autocomplete-item{padding:11px 13px;cursor:pointer;border-bottom:1px solid #f0f0f0}
.autocomplete-item:hover{background:#f5f3ff}
@media(max-width:600px){.support-float{right:12px;bottom:12px}.support-box{width:260px}}
@media(max-width:600px){.top{flex-direction:column}.table-wrap{max-height:none}}
</style>
<style>
body.dark{background:#151522;color:#eee}
body.dark header{background:linear-gradient(135deg,#24134f,#3d1d78)}
body.dark .box,body.dark table,body.dark .autocomplete-list{background:#222233;color:#eee}
body.dark input,body.dark textarea,body.dark select{background:#29293b;color:#fff;border-color:#555}
body.dark th{background:#302b4b}
body.dark td{border-color:#444}
body.dark .muted,.dark .hint{color:#bbb}
body.dark .modal{background:rgba(0,0,0,.72)}
body.dark .empty{background:#222233}
.extra-tools{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:8px;margin:12px 0}
.extra-tools button{border:0;border-radius:10px;padding:10px 8px;cursor:pointer;font-weight:bold;font-size:13px;min-height:42px}
@media(max-width:520px){.extra-tools{grid-template-columns:1fr 1fr}.extra-tools button{font-size:12px;padding:9px 6px}}
.info-modal .box{max-width:760px}
.simple-list{display:flex;flex-direction:column;gap:7px;max-height:60vh;overflow:auto}
.simple-row{display:flex;align-items:center;justify-content:space-between;gap:8px;padding:9px 10px;border:1px solid #ddd;border-radius:10px;background:rgba(255,255,255,.55)}
.dark .simple-row{border-color:#555}
.simple-row .main{min-width:0}
.simple-row .main b{display:block;margin-bottom:4px}
.simple-row .small{font-size:13px;color:#777}
.dark .simple-row .small{color:#bbb}
.invoice-card{border:2px solid #ddd;border-radius:14px;padding:18px;background:#fff;color:#222}
.dark .invoice-card{background:#29293b;color:#fff;border-color:#555}
.invoice-head{text-align:center;border-bottom:1px dashed #aaa;padding-bottom:10px;margin-bottom:12px}
.invoice-line{display:flex;justify-content:space-between;gap:10px;padding:7px 0;border-bottom:1px solid #eee}
.dark .invoice-line{border-color:#444}
.invoice-actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:14px}
.invoice-actions button{padding:11px 14px;border:0;border-radius:10px;cursor:pointer;font-weight:bold}
</style>
</head><body>
<header><div class="wrap"><div class="top"><div class="logo">🔧 مدیریت کالاهای تعمیری</div><div>مدیریت کالا و تعمیر</div></div>
<div id="todayDisplay" style="margin-top:14px;font-size:24px;font-weight:bold;text-align:center">امروز: —</div><div class="search"><span>🔎</span><input id="search" placeholder="جستجوی کد کالا..."></div></div></header>
<main><div class="buttons"><button class="add" id="addBtn">➕ افزودن کالا</button><button class="tab active" data-f="repairing">🔧 تعمیری‌ها</button><button class="tab" data-f="repaired">✅ تعمیر شده‌ها</button><button class="tab" data-f="all">📦 همه کالاها</button></div><div class="extra-tools"><button onclick="invoiceByCode()">📄 فاکتور</button><button onclick="showNotDelivered()">📦 تحویل نگرفته‌ها</button><button onclick="showUnpriced()">🔧 لیست برای تعمیرکننده</button><button onclick="toggleDark()">🌙 حالت شب</button></div><h2 id="title">🔧 کالاهای تعمیری</h2><div id="cards" class="cards"></div></main>
<div id="addModal" class="modal"><div class="box">
<h2>➕ افزودن کالا</h2>
<div class="group"><label>نام شخص <span class="required">*</span></label><div class="autocomplete-wrap"><input id="person" autocomplete="off"><div id="personSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>نام کالا <span class="required">*</span></label><div class="autocomplete-wrap"><input id="name" autocomplete="off"><div id="nameSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>اطلاعات کالا</label><div class="autocomplete-wrap"><textarea id="info" placeholder="توضیحات کامل کالا را وارد کنید..."></textarea><div id="infoSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>شماره موبایل</label><div class="autocomplete-wrap"><input id="mobile" inputmode="tel" autocomplete="tel" placeholder="مثلاً ۰۹۱۲۱۲۳۴۵۶۷"><div id="mobileSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>📅 تاریخ</label><select id="addDate" style="width:100%;padding:13px;border:1px solid #ddd;border-radius:10px;font:inherit;min-height:52px"></select><span class="hint">از ۲۲ شهریور ۱۴۰۵ تا ۲۲ شهریور ۱۴۰۶</span></div>
<div class="modal-actions"><button class="save" id="save">ثبت کالا</button><button class="cancel" id="cancel">لغو</button></div>
</div></div>
<div id="editModal" class="modal"><div class="box">
<h2>✏️ ویرایش کالا</h2>
<div class="group"><label>نام شخص <span class="required">*</span></label><div class="autocomplete-wrap"><input id="editPerson" autocomplete="off"><div id="editPersonSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>نام کالا <span class="required">*</span></label><div class="autocomplete-wrap"><input id="editName" autocomplete="off"><div id="editNameSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>اطلاعات کالا</label><div class="autocomplete-wrap"><textarea id="editInfo" placeholder="توضیحات کامل کالا را وارد کنید..."></textarea><div id="editInfoSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>شماره موبایل</label><div class="autocomplete-wrap"><input id="editMobile" inputmode="tel" autocomplete="tel"><div id="editMobileSuggestions" class="autocomplete-list"></div></div></div>
<div class="group"><label>📅 تاریخ ثبت</label><select id="editDate" style="width:100%;padding:13px;border:1px solid #ddd;border-radius:10px;font:inherit;min-height:52px"></select></div>
<div class="group"><label>💰 قیمت تعمیر</label><input id="editPrice" inputmode="numeric" placeholder="مثلاً 250000"><span class="hint">اگر قیمت را وارد کنید، وضعیت کالا «تعمیر شد» می‌شود.</span><div id="editPriceWords" class="price-words"></div></div>
<div class="group"><label>📅 تاریخ تحویل</label><select id="editDeliveryDate" style="width:100%;padding:13px;border:1px solid #ddd;border-radius:10px;font:inherit;min-height:52px"></select></div>
<div class="modal-actions"><button class="save" id="saveEdit">ذخیره تغییرات</button><button class="cancel" id="cancelEdit">لغو</button></div>
</div></div>
<div id="priceModal" class="modal"><div class="box">
<h2>💰 ثبت قیمت تعمیر</h2>
<div class="group"><label>قیمت تعمیر <span class="required">*</span></label><input id="price" inputmode="numeric" placeholder="مثلاً 250000"><span class="hint">مبلغ را به تومان وارد کنید.</span><div id="priceWords" class="price-words"></div></div>
<div class="modal-actions"><button class="save" id="savePrice">ثبت قیمت و تعمیر شد</button><button class="cancel" id="cancelPrice">لغو</button></div>
</div></div>
<div id="deliveryModal" class="modal"><div class="box">
<h2>📅 تاریخ تحویل</h2>
<div class="group"><label>تاریخ تحویل</label><select id="deliveryDate" style="width:100%;padding:13px;border:1px solid #ddd;border-radius:10px;font:inherit;min-height:52px"></select><span class="hint">از ۲۲ شهریور ۱۴۰۵ تا ۲۲ شهریور ۱۴۰۶</span></div>
<div class="modal-actions"><button class="save" id="saveDelivery">ذخیره تاریخ</button><button class="cancel" id="cancelDelivery">لغو</button></div>
</div></div></div>

<div id="invoiceModal" class="modal info-modal"><div class="box">
<h2>📄 فاکتور</h2><div id="invoiceContent"></div>
<div class="modal-actions"><button class="cancel" onclick="hide('invoiceModal')">بستن</button></div>
</div></div>
<div id="notDeliveredModal" class="modal info-modal"><div class="box">
<h2>📦 تحویل نگرفته‌ها</h2>
<div class="extra-tools"><button onclick="downloadNotDelivered(false)">🖼️ دانلود تکی</button><button onclick="downloadNotDelivered(true)">📥 دانلود کل جدول</button></div>
<div id="notDeliveredList" class="simple-list"></div>
<div class="modal-actions"><button class="cancel" onclick="hide('notDeliveredModal')">بستن</button></div>
</div></div>
<div id="unpricedModal" class="modal info-modal"><div class="box">
<h2>🔧 لیست برای تعمیرکننده</h2>
<div class="extra-tools"><button onclick="downloadUnpriced(false)">🖼️ دانلود تکی</button><button onclick="downloadUnpriced(true)">📥 دانلود کل جدول</button></div>
<div id="unpricedList" class="simple-list"></div>
<div class="modal-actions"><button class="cancel" onclick="hide('unpricedModal')">بستن</button></div>
</div></div>
<div class="support-float">
<button class="support-btn" id="supportBtn" aria-label="پشتیبانی">💬</button>
<div class="support-box" id="supportBox">
<b>سلام، یوسف هستم 👋</b><br>
کمک خاصی خواستی با این شماره تماس یا پیام بده:<br>
<a href="tel:09134860153">📞 09134860153</a>
</div>
</div>
<script>
document.getElementById('supportBtn').onclick=()=>document.getElementById('supportBox').classList.toggle('show');
const LS_ITEMS='kalaTaeemItems_v1',LS_USED='kalaTaeemUsedCodes_v1',LS_MIGRATED='kalaTaeemMigratedFromIDB_v1';let items=[],filter='repairing',current=null;
function readLS(key,fallback){try{const raw=localStorage.getItem(key);return raw!==null?JSON.parse(raw):fallback}catch(e){return fallback}}
function writeLS(key,val){try{localStorage.setItem(key,JSON.stringify(val));return true}catch(e){return false}}
function loadItemsFromStorage(){
  const arr=readLS(LS_ITEMS,[]); const map=new Map();
  arr.forEach(x=>{const k=x.code!=null&&String(x.code)!==''?'code:'+normalizeCode(x.code):'id:'+String(x.id); map.set(k,x)});
  const clean=Array.from(map.values()); if(clean.length!==arr.length) writeLS(LS_ITEMS,clean); return clean;
}
function saveItemsToStorage(arr){writeLS(LS_ITEMS,arr)}
function loadUsedCodes(){return readLS(LS_USED,[])}
function saveUsedCodes(arr){writeLS(LS_USED,arr)}
function nextId(){const arr=loadItemsFromStorage();let max=0;arr.forEach(x=>{if(typeof x.id==='number'&&x.id>max)max=x.id});return max+1}
function all(){return Promise.resolve(loadItemsFromStorage())}
function put(x){let arr=loadItemsFromStorage(),code=normalizeCode(x.code),id=Number(x.id);arr=arr.filter(a=>Number(a.id)!==id&&!(code&&normalizeCode(a.code)===code));arr.push(x);saveItemsToStorage(arr);return Promise.resolve()}
function add(x){let arr=loadItemsFromStorage();if(arr.some(a=>normalizeCode(a.code)===normalizeCode(x.code)))return Promise.resolve();x.id=nextId();arr.push(x);saveItemsToStorage(arr);return Promise.resolve()}
function del(id){let arr=loadItemsFromStorage().filter(a=>a.id!==id);saveItemsToStorage(arr);return Promise.resolve()}
function migrateFromIndexedDB(){return new Promise(resolve=>{try{if(localStorage.getItem(LS_MIGRATED)){resolve();return}if(!('indexedDB' in window)){writeLS(LS_MIGRATED,true);resolve();return}const req=indexedDB.open('KalaTaeemDB');let created=false;req.onupgradeneeded=e=>{created=true;try{e.target.transaction.abort()}catch(_){}};req.onsuccess=e=>{const d=e.target.result;if(created||!d.objectStoreNames.contains('products')){writeLS(LS_MIGRATED,true);try{d.close()}catch(_){}resolve();return}try{const tx=d.transaction('products','readonly');const gr=tx.objectStore('products').getAll();gr.onsuccess=()=>{const oldItems=gr.result||[];if(oldItems.length&&loadItemsFromStorage().length===0){saveItemsToStorage(oldItems)}if(d.objectStoreNames.contains('usedCodes')){const tx2=d.transaction('usedCodes','readonly');const gu=tx2.objectStore('usedCodes').getAll();gu.onsuccess=()=>{const oldUsed=(gu.result||[]).map(x=>x.code);if(oldUsed.length){const merged=Array.from(new Set([...loadUsedCodes(),...oldUsed]));saveUsedCodes(merged)}writeLS(LS_MIGRATED,true);try{d.close()}catch(_){}resolve()};gu.onerror=()=>{writeLS(LS_MIGRATED,true);try{d.close()}catch(_){}resolve()}}else{writeLS(LS_MIGRATED,true);try{d.close()}catch(_){}resolve()}};gr.onerror=()=>{writeLS(LS_MIGRATED,true);try{d.close()}catch(_){}resolve()}}catch(e2){writeLS(LS_MIGRATED,true);resolve()}};req.onerror=()=>{writeLS(LS_MIGRATED,true);resolve()}}catch(e){resolve()}})}
const faDigits='۰۱۲۳۴۵۶۷۸۹';
function faNum(v){return String(v??'').replace(/\d/g,d=>faDigits[d])}
function enNum(v){return String(v??'').replace(/[۰-۹]/g,d=>String(faDigits.indexOf(d))).replace(/[٠-٩]/g,d=>String('٠١٢٣٤٥٦٧٨٩'.indexOf(d)))}
function normalize(v){return enNum(v).toLocaleLowerCase('fa-IR').replace(/\s+/g,' ').trim()}
function normalizeMobile(v){return enNum(v).replace(/\D/g,'')}
function normalizeCode(v){return enNum(v).replace(/\D/g,'')}
function esc(x){return String(x??'').replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]))}
async function uniqueCode(){const used=new Set(items.map(x=>String(x.code)));const old=loadUsedCodes().map(String);old.forEach(x=>used.add(x));if(used.size>=9000)throw Error('full');let n,guard=0;do{n=String(Math.floor(1000+Math.random()*9000));guard++}while(used.has(n)&&guard<20000);if(used.has(n))for(let i=1000;i<=9999;i++)if(!used.has(String(i))){n=String(i);break}const merged=Array.from(new Set([...old,n]));saveUsedCodes(merged);return n}
function isoDate(d){return new Date(d.getTime()-d.getTimezoneOffset()*60000).toISOString().slice(0,10)}
function setupDateInput(id, selected=''){
  let el=document.getElementById(id);if(!el)return;
  let start=new Date('2026-09-13T00:00:00'), end=new Date('2027-09-13T00:00:00');
  el.innerHTML='<option value="">انتخاب تاریخ</option>';
  for(let d=new Date(start);d<=end;d.setDate(d.getDate()+1)){
    let v=isoDate(d),o=document.createElement('option');o.value=v;o.textContent=persianDate(d);el.appendChild(o)
  }
  if(selected)el.value=selected;
}
function persianDateInput(v){if(!v)return '';let p=new Intl.DateTimeFormat('fa-IR-u-ca-persian',{year:'numeric',month:'numeric',day:'numeric'}).formatToParts(new Date(v+'T00:00:00')),g=k=>p.find(x=>x.type===k)?.value||'';return `${g('year')}/${g('month')}/${g('day')}`}
function persianDate(d=new Date()){const p=new Intl.DateTimeFormat('fa-IR-u-ca-persian',{year:'numeric',month:'2-digit',day:'2-digit'}).formatToParts(d),g=k=>p.find(x=>x.type===k)?.value||'';return `${g('year')}/${g('month')}/${g('day')}`}
function formatMoney(v){return Number(v).toLocaleString('fa-IR')+' تومان'}
const ones=['صفر','یک','دو','سه','چهار','پنج','شش','هفت','هشت','نه','ده','یازده','دوازده','سیزده','چهارده','پانزده','شانزده','هفده','هجده','نوزده'],tens=['','','بیست','سی','چهل','پنجاه','شصت','هفتاد','هشتاد','نود'],hundreds=['','صد','دویست','سیصد','چهارصد','پانصد','ششصد','هفتصد','هشتصد','نهصد'],scales=['','هزار','میلیون','میلیارد','تریلیون','کوادریلیون'];
function under1000(n){let a=[];if(Math.floor(n/100))a.push(hundreds[Math.floor(n/100)]),n%=100;if(n){if(n<20)a.push(ones[n]);else{a.push(tens[Math.floor(n/10)]);if(n%10)a.push(ones[n%10])}}return a.join(' و ')}
function numberToWords(n){n=Math.floor(Number(n));if(!Number.isFinite(n)||n<0)return '';if(n===0)return 'صفر';let a=[],i=0;while(n>0){let x=n%1000;if(x)a.unshift(under1000(x)+(scales[i]?' '+scales[i]:''));n=Math.floor(n/1000);i++}return a.join(' و ')}
function render(){let seenIds=new Set(),seenCodes=new Set(),dedupItems=items.filter(x=>{let ik='id:'+String(x.id),ck=x.code!=null&&String(x.code)!==''?'code:'+normalizeCode(x.code):null;if(seenIds.has(ik)||(ck&&seenCodes.has(ck)))return false;seenIds.add(ik);if(ck)seenCodes.add(ck);return true}),q=normalize(document.getElementById('search').value),qc=normalizeCode(q),qm=normalizeMobile(q),a=dedupItems.filter(x=>(filter==='all'||x.status===filter)&&(!q||normalize(x.person).includes(q)||normalize(x.name).includes(q)||normalizeCode(x.code).includes(qc)||normalizeMobile(x.mobile).includes(qm))),c=document.getElementById('cards');if(!a.length){c.innerHTML='<div class="empty">📦<h3>کالایی پیدا نشد</h3></div>';return}c.innerHTML=`<div class="table-wrap"><table><thead><tr><th>نام شخص</th><th>کد</th><th>نام کالا</th><th>اطلاعات کالا</th><th>تاریخ ثبت</th><th>تاریخ تحویل</th><th>شماره موبایل</th><th>وضعیت</th><th>قیمت</th><th>عملیات</th></tr></thead><tbody>${a.map(x=>`<tr><td>${esc(x.person)}</td><td><span class="code">${faNum(x.code)}</span></td><td>${esc(x.name)}</td><td>${esc(x.info||'بدون توضیحات')}</td><td>${esc(x.createdAt)}${x.addDate&&persianDateInput(x.addDate)!==x.createdAt?'<div class="muted">📅 تاریخ انتخابی: '+esc(persianDateInput(x.addDate))+'</div>':''}</td><td>${esc(x.deliveryDate?persianDateInput(x.deliveryDate):'-')}</td><td>${esc(faNum(x.mobile))}</td><td><span class="status ${x.status}">${x.status==='repaired'?'✅ تعمیر شد':'🔧 تعمیری'}</span>${x.deliveryDate?'<div class="muted">📅 تحویل: '+esc(persianDateInput(x.deliveryDate))+'</div>':''}</td><td>${x.price!==null&&x.price!==undefined?'<div class="price">💰 '+formatMoney(x.price)+'</div>':(x.status==='repairing'?'<button class="repair" onclick="priceModal('+x.id+')">💰 ثبت قیمت</button>':'')}</td><td><div class="actions"><button class="edit" onclick="editModal(${x.id})">✏️ ویرایش</button><button class="tab" onclick="deliveryModal(${x.id})">📅 تاریخ تحویل</button><button class="tab" onclick="openInvoice(${x.id})">📄 فاکتور</button><button class="tab" onclick="shareItemImage(${x.id})">🖼️ ارسال عکس</button><button class="del" onclick="removeItem(${x.id})">🗑️ حذف</button></div></td></tr>`).join('')}</tbody></table></div>`}
function setFilter(f){filter=f;document.querySelectorAll('.tab').forEach(b=>b.classList.toggle('active',b.dataset.f===f));document.getElementById('title').textContent=f==='repairing'?'🔧 کالاهای تعمیری':f==='repaired'?'✅ تعمیر شده‌ها':'📦 همه کالاها';render()}
function show(id){document.getElementById(id).classList.add('show')}function hide(id){document.getElementById(id).classList.remove('show')}
document.getElementById('addBtn').onclick=()=>{setupDateInput('addDate',isoDate(new Date()));show('addModal')};document.getElementById('cancel').onclick=()=>hide('addModal');document.getElementById('cancelPrice').onclick=()=>hide('priceModal');document.getElementById('search').oninput=render;document.querySelectorAll('.tab').forEach(b=>b.onclick=()=>setFilter(b.dataset.f));
document.getElementById('save').onclick=async()=>{let person=document.getElementById('person').value.trim(),name=document.getElementById('name').value.trim(),info=document.getElementById('info').value,mobile=normalizeMobile(document.getElementById('mobile').value),addDate=document.getElementById('addDate').value;if(!person)return alert('لطفاً نام شخص را وارد کنید.');if(!name)return alert('لطفاً نام کالا را وارد کنید.');if(mobile&&mobile.length<7)return alert('لطفاً شماره موبایل معتبر وارد کنید.');try{let c=await uniqueCode(),x={code:c,name,person,info,mobile,price:null,priceWords:'',status:'repairing',createdAt:persianDate(),addDate:addDate||isoDate(new Date()),deliveryDate:''};let ok=confirm('اطلاعات شما درست هست؟\\n\\nنام شخص: '+(x.person||'—')+'\\nنام کالا: '+(x.name||'—')+'\\nاطلاعات: '+(x.info||'—')+'\\nشماره: '+(x.mobile?faNum(x.mobile):'—')+'\\nتاریخ: '+(x.addDate?persianDateInput(x.addDate):'—')+'\\n\\nاین کالا ثبت شود؟');if(!ok)return;await add(x);items=await all();hide('addModal');['name','person','info','mobile'].forEach(id=>document.getElementById(id).value='');setupDateInput('addDate',isoDate(new Date()));setFilter('repairing');alert('آقای حمید گل 🌷 این کد شماست: '+faNum(x.code)+' . اطلاعات این جنس با موفقیت ثبت شد.')}catch(e){alert('ثبت کالا انجام نشد. دوباره تلاش کنید.')}}
window.priceModal=id=>{current=id;document.getElementById('price').value='';document.getElementById('priceWords').textContent='';show('priceModal')}
document.getElementById('price').oninput=()=>{let v=normalizeCode(document.getElementById('price').value);document.getElementById('priceWords').textContent=v?numberToWords(v)+' تومان':''}
document.getElementById('savePrice').onclick=async()=>{let v=normalizeCode(document.getElementById('price').value);if(v===''||!Number.isFinite(Number(v))||Number(v)<0)return alert('لطفاً قیمت را به تومان وارد کنید.');let x=items.find(a=>Number(a.id)===Number(current));if(!x)return;x.price=Number(v);x.priceWords=numberToWords(x.price)+' تومان';x.status='repaired';await put(x);items=await all();hide('priceModal');setFilter('repaired')} 

function setupAutocomplete(inputId,listId,key,mode='text'){
  const input=document.getElementById(inputId),list=document.getElementById(listId);
  if(!input||!list)return;
  const draw=()=>{
    const q=normalize(input.value);
    const vals=Array.from(new Set(items.map(x=>String(x[key]??'').trim()).filter(Boolean)))
      .filter(v=>!q||normalize(v).includes(q)).slice(0,8);
    if(!vals.length){list.classList.remove('show');list.innerHTML='';return}
    list.innerHTML=vals.map(v=>'<div class="autocomplete-item" data-v="'+esc(v)+'">'+esc(v)+'</div>').join('');
    list.classList.add('show');
    list.querySelectorAll('.autocomplete-item').forEach(el=>el.onclick=()=>{
      input.value=el.dataset.v;list.classList.remove('show');list.innerHTML='';
    });
  };
  input.addEventListener('input',draw);
  input.addEventListener('focus',draw);
  input.addEventListener('blur',()=>setTimeout(()=>list.classList.remove('show'),180));
}
setupAutocomplete('person','personSuggestions','person');
setupAutocomplete('name','nameSuggestions','name');
setupAutocomplete('info','infoSuggestions','info');
setupAutocomplete('mobile','mobileSuggestions','mobile');
setupAutocomplete('editPerson','editPersonSuggestions','person');
setupAutocomplete('editName','editNameSuggestions','name');
setupAutocomplete('editInfo','editInfoSuggestions','info');
setupAutocomplete('editMobile','editMobileSuggestions','mobile');

window.editModal=id=>{
  current=id;let x=items.find(a=>Number(a.id)===Number(id));if(!x)return;
  document.getElementById('editPerson').value=x.person||'';
  document.getElementById('editName').value=x.name||'';
  document.getElementById('editInfo').value=x.info||'';
  document.getElementById('editMobile').value=x.mobile||'';
  setupDateInput('editDate',x.addDate||isoDate(new Date()));
  document.getElementById('editPrice').value=x.price!==null&&x.price!==undefined?String(x.price):'';
  document.getElementById('editPriceWords').textContent=x.price!==null&&x.price!==undefined?numberToWords(x.price)+' تومان':'';
  setupDateInput('editDeliveryDate',x.deliveryDate||'');
  show('editModal');
};
document.getElementById('cancelEdit').onclick=()=>hide('editModal');
document.getElementById('saveEdit').onclick=async()=>{
  let x=items.find(a=>Number(a.id)===Number(current));if(!x)return;
  let person=document.getElementById('editPerson').value.trim();
  let name=document.getElementById('editName').value.trim();
  let info=document.getElementById('editInfo').value;
  let mobile=normalizeMobile(document.getElementById('editMobile').value);
  let addDate=document.getElementById('editDate').value;
  let priceRaw=normalizeCode(document.getElementById('editPrice').value);
  let deliveryDate=document.getElementById('editDeliveryDate').value;
  if(!person)return alert('لطفاً نام شخص را وارد کنید.');
  if(!name)return alert('لطفاً نام کالا را وارد کنید.');
  if(mobile&&mobile.length<7)return alert('لطفاً شماره موبایل معتبر وارد کنید.');
  if(priceRaw!==''&&(!Number.isFinite(Number(priceRaw))||Number(priceRaw)<0))return alert('لطفاً قیمت را به تومان وارد کنید.');
  x.person=person;x.name=name;x.info=info;x.mobile=mobile;
  if(addDate)x.addDate=addDate;
  if(priceRaw===''){x.price=null;x.priceWords='';x.status='repairing'}
  else{x.price=Number(priceRaw);x.priceWords=numberToWords(x.price)+' تومان';x.status='repaired'}
  x.deliveryDate=deliveryDate||'';
  await put(x);items=await all();hide('editModal');render();
};

document.getElementById('editPrice').oninput=()=>{let v=normalizeCode(document.getElementById('editPrice').value);document.getElementById('editPriceWords').textContent=v?numberToWords(v)+' تومان':''};
window.deliveryModal=id=>{
  current=id;let x=items.find(a=>a.id===id);
  setupDateInput('deliveryDate',x?.deliveryDate||isoDate(new Date()));
  show('deliveryModal')
}
document.getElementById('cancelDelivery').onclick=()=>hide('deliveryModal')
document.getElementById('saveDelivery').onclick=async()=>{let v=document.getElementById('deliveryDate').value;if(!v)return alert('لطفاً تاریخ تحویل را انتخاب کنید.');let x=items.find(a=>a.id===current);if(!x)return;x.deliveryDate=v;await put(x);items=await all();hide('deliveryModal');render()}

window.removeItem=async id=>{if(confirm('آیا از حذف این کالا مطمئن هستید؟')){await del(id);items=await all();render()}}
function updateTodayDisplay(){
  const el=document.getElementById('todayDisplay');
  if(el)el.textContent='امروز: '+persianDate(new Date());
}
updateTodayDisplay();
setInterval(updateTodayDisplay,60000);


function toggleDark(){document.body.classList.toggle('dark');localStorage.setItem('kalaDarkMode',document.body.classList.contains('dark')?'1':'0')}
if(localStorage.getItem('kalaDarkMode')==='1')document.body.classList.add('dark');

function itemText(x){
  return 'فاکتور تعمیرات\nکد: '+faNum(x.code)+'\nنام شخص: '+(x.person||'—')+'\nنام کالا: '+(x.name||'—')+'\nاطلاعات: '+(x.info||'—')+'\nشماره: '+(x.mobile?faNum(x.mobile):'—')+'\nوضعیت: '+(x.status==='repaired'?'تعمیر شد':'در حال تعمیر')+'\nقیمت: '+(x.price!==null&&x.price!==undefined?formatMoney(x.price):'ثبت نشده');
}
function shareText(text,title='اطلاعات تعمیر'){
  if(navigator.share){navigator.share({title,text}).catch(()=>{})}
  else if(navigator.clipboard){navigator.clipboard.writeText(text);alert('اطلاعات کپی شد؛ حالا می‌توانید برای شخص ارسال کنید.')}
  else alert(text);
}
window.invoiceByCode=()=>{
  let q=prompt('کد ۴ رقمی کالا را وارد کنید:');if(!q)return;
  q=normalizeCode(q);let x=items.find(a=>normalizeCode(a.code)===q);
  if(!x)return alert('کالایی با این کد پیدا نشد.');
  openInvoice(x.id);
};
window.openInvoice=id=>{
  let x=items.find(a=>Number(a.id)===Number(id));if(!x)return;
  document.getElementById('invoiceContent').innerHTML='<div class="invoice-card"><div class="invoice-head"><h2>فاکتور تعمیرات</h2><div>کد: <b>'+faNum(x.code)+'</b></div></div>'+
    '<div class="invoice-line"><span>نام شخص</span><b>'+esc(x.person||'—')+'</b></div>'+
    '<div class="invoice-line"><span>نام کالا</span><b>'+esc(x.name||'—')+'</b></div>'+
    '<div class="invoice-line"><span>اطلاعات</span><b>'+esc(x.info||'—')+'</b></div>'+
    '<div class="invoice-line"><span>شماره</span><b>'+esc(faNum(x.mobile||'—'))+'</b></div>'+
    '<div class="invoice-line"><span>وضعیت</span><b>'+(x.status==='repaired'?'تعمیر شد':'در حال تعمیر')+'</b></div>'+
    '<div class="invoice-line"><span>قیمت</span><b>'+(x.price!==null&&x.price!==undefined?formatMoney(x.price):'ثبت نشده')+'</b></div>'+
    '<div class="invoice-actions"><button onclick="printInvoice('+x.id+')">🖨️ چاپ</button><button onclick="shareInvoice('+x.id+')">📤 ارسال فاکتور</button></div></div>';
  show('invoiceModal');
};
window.downloadInvoice=id=>{
  let x=items.find(a=>Number(a.id)===Number(id));if(!x)return;
  let canvas=document.createElement('canvas'),ctx=canvas.getContext('2d');canvas.width=1000;canvas.height=760;
  ctx.fillStyle='#fff';ctx.fillRect(0,0,1000,760);ctx.fillStyle='#222';ctx.direction='rtl';ctx.textAlign='right';
  ctx.font='bold 40px Tahoma';ctx.fillText('فاکتور تعمیرات',900,65);
  ctx.font='bold 26px Tahoma';ctx.fillText('کد: '+faNum(x.code),900,110);
  ctx.font='23px Tahoma';
  [['نام شخص',x.person||'—'],['نام کالا',x.name||'—'],['اطلاعات',x.info||'—'],['شماره',x.mobile?faNum(x.mobile):'—'],['وضعیت',x.status==='repaired'?'تعمیر شد':'در حال تعمیر'],['قیمت',x.price!==null&&x.price!==undefined?formatMoney(x.price):'ثبت نشده']].forEach((r,i)=>ctx.fillText(r[0]+': '+String(r[1]),900,175+i*70));
  ctx.font='18px Tahoma';ctx.fillText('مدیریت کالاهای تعمیری',900,710);
  canvas.toBlob(blob=>{if(!blob)return;let a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='فاکتور-'+x.code+'.png';a.click();setTimeout(()=>URL.revokeObjectURL(a.href),1000)},'image/png');
};
window.printInvoice=id=>{
  let x=items.find(a=>Number(a.id)===Number(id));if(!x)return;
  let w=window.open('','_blank','width=700,height=800');if(!w)return alert('اجازه باز شدن پنجره چاپ را بدهید.');
  w.document.write('<html dir="rtl"><head><meta charset="utf-8"><title>فاکتور '+faNum(x.code)+'</title><style>body{font-family:Tahoma;padding:30px}h1{text-align:center}.line{display:flex;justify-content:space-between;padding:10px;border-bottom:1px solid #ddd}</style></head><body><h1>فاکتور تعمیرات</h1><p style="text-align:center">کد: '+faNum(x.code)+'</p>'+
  '<div class="line"><span>نام شخص</span><b>'+esc(x.person||'—')+'</b></div><div class="line"><span>نام کالا</span><b>'+esc(x.name||'—')+'</b></div><div class="line"><span>اطلاعات</span><b>'+esc(x.info||'—')+'</b></div><div class="line"><span>شماره</span><b>'+esc(faNum(x.mobile||'—'))+'</b></div><div class="line"><span>وضعیت</span><b>'+(x.status==='repaired'?'تعمیر شد':'در حال تعمیر')+'</b></div><div class="line"><span>قیمت</span><b>'+(x.price!==null&&x.price!==undefined?formatMoney(x.price):'ثبت نشده')+'</b></div></body></html>');w.document.close();w.focus();setTimeout(()=>w.print(),300);
};
window.shareInvoice=id=>{let x=items.find(a=>Number(a.id)===Number(id));if(x)shareText(itemText(x),'فاکتور تعمیرات '+faNum(x.code))};

function tableDownload(rows,title,headers,includePersonPrice){
  let canvas=document.createElement('canvas'),ctx=canvas.getContext('2d');
  let rowH=70,headH=120,pad=40,width=1100,height=Math.max(300,headH+rows.length*rowH+pad*2);
  canvas.width=width;canvas.height=height;
  ctx.fillStyle='#fff';ctx.fillRect(0,0,width,height);ctx.fillStyle='#222';ctx.direction='rtl';ctx.textAlign='right';
  ctx.font='bold 38px Tahoma';ctx.fillText(title,width-pad,55);
  ctx.font='bold 25px Tahoma';
  let cols=includePersonPrice?['نام شخص','نام کالا','قیمت']:headers;
  let xs=includePersonPrice?[1000,650,280]:[1000,500];
  cols.forEach((h,i)=>ctx.fillText(h,xs[i],100));
  ctx.font='23px Tahoma';
  rows.forEach((r,idx)=>{
    let y=headH+(idx+1)*rowH;ctx.strokeStyle='#ddd';ctx.beginPath();ctx.moveTo(pad,y+15);ctx.lineTo(width-pad,y+15);ctx.stroke();
    let vals=includePersonPrice?[r.person||'—',r.name||'—',(r.price!==null&&r.price!==undefined)?formatMoney(r.price):'—']:r;
    vals.forEach((v,i)=>ctx.fillText(String(v),xs[i],y));
  });
  ctx.font='18px Tahoma';ctx.fillText('مدیریت کالاهای تعمیری',width-pad,height-20);
  canvas.toBlob(blob=>{if(!blob)return;let a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download=title.replace(/\s+/g,'-')+'.png';a.click();setTimeout(()=>URL.revokeObjectURL(a.href),1000)},'image/png');
}
window.showNotDelivered=()=>{
  let a=items.filter(x=>!x.deliveryDate),list=document.getElementById('notDeliveredList');
  if(!a.length)list.innerHTML='<div class="empty">همه کالاها تحویل داده شده‌اند.</div>';
  else list.innerHTML='<div class="simple-list">'+a.map(x=>'<div class="simple-row"><div class="main"><b>'+esc(x.person||'—')+'</b><div class="small">کالا: '+esc(x.name||'—')+(x.price!==null&&x.price!==undefined?' | قیمت: '+formatMoney(x.price):'')+'</div></div><button onclick="downloadNotDeliveredItem('+x.id+')">📥 دانلود</button></div>').join('')+'</div>';
  show('notDeliveredModal');
};
window.downloadNotDeliveredItem=id=>{let x=items.find(a=>Number(a.id)===Number(id));if(x)tableDownload([x],'کالای تحویل‌نگرفته',['نام شخص','نام کالا'],true)};
window.downloadNotDelivered=allRows=>{let a=items.filter(x=>!x.deliveryDate);if(!a.length)return alert('کالایی برای دانلود وجود ندارد.');if(allRows)tableDownload(a,'کالاهای تحویل‌نگرفته',['نام شخص','نام کالا'],true);else downloadNotDeliveredItem(a[0].id)};

window.showUnpriced=()=>{
  let a=items.filter(x=>x.price===null||x.price===undefined||x.price===''),list=document.getElementById('unpricedList');
  if(!a.length)list.innerHTML='<div class="empty">همه کالاها قیمت دارند.</div>';
  else list.innerHTML='<div class="simple-list">'+a.map(x=>'<div class="simple-row"><div class="main"><b>'+esc(x.name||'—')+'</b><div class="small">کد: '+faNum(x.code)+'</div></div><button onclick="downloadUnpricedItem('+x.id+')">📥 دانلود</button></div>').join('')+'</div>';
  show('unpricedModal');
};
window.downloadUnpricedItem=id=>{let x=items.find(a=>Number(a.id)===Number(id));if(x)tableDownload([[x.name||'—',faNum(x.code)]],'برای تعمیرکننده',['نام کالا','کد'],false)};
window.downloadUnpriced=allRows=>{let a=items.filter(x=>x.price===null||x.price===undefined||x.price==='');if(!a.length)return alert('کالای بدون قیمت وجود ندارد.');if(allRows)tableDownload(a.map(x=>[x.name||'—',faNum(x.code)]),'برای تعمیرکننده',['نام کالا','کد'],false);else downloadUnpricedItem(a[0].id)};

window.shareItemImage=async id=>{
  let x=items.find(a=>Number(a.id)===Number(id));if(!x)return;
  let canvas=document.createElement('canvas'),ctx=canvas.getContext('2d');canvas.width=1000;canvas.height=700;
  ctx.fillStyle='#ffffff';ctx.fillRect(0,0,1000,700);ctx.fillStyle='#222';ctx.direction='rtl';ctx.textAlign='right';
  ctx.font='bold 42px Tahoma';ctx.fillText('فاکتور تعمیرات',900,70);
  ctx.font='bold 32px Tahoma';ctx.fillText('کد: '+faNum(x.code),900,130);
  ctx.font='28px Tahoma';ctx.fillText('نام شخص: '+(x.person||'—'),900,200);ctx.fillText('نام کالا: '+(x.name||'—'),900,260);
  ctx.fillText('اطلاعات: '+(x.info||'—').slice(0,45),900,320);ctx.fillText('وضعیت: '+(x.status==='repaired'?'تعمیر شد':'در حال تعمیر'),900,380);
  ctx.fillText('قیمت: '+(x.price!==null&&x.price!==undefined?formatMoney(x.price):'ثبت نشده'),900,440);
  ctx.fillText('شماره: '+(x.mobile?faNum(x.mobile):'—'),900,500);
  ctx.font='22px Tahoma';ctx.fillText('مدیریت کالاهای تعمیری',900,620);
  canvas.toBlob(async blob=>{
    if(!blob)return;
    let file=new File([blob],'factor-'+x.code+'.png',{type:'image/png'});
    if(navigator.share && navigator.canShare && navigator.canShare({files:[file]})){try{await navigator.share({title:'فاکتور تعمیرات',files:[file]});return}catch(e){}}
    let a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='factor-'+x.code+'.png';a.click();URL.revokeObjectURL(a.href);alert('عکس فاکتور آماده شد و در دستگاه ذخیره شد.');
  },'image/png');
};

(async()=>{try{await migrateFromIndexedDB();items=await all();for(const x of items){let ch=false;if(x.mobile===undefined){x.mobile='';ch=true}if(x.createdAt===undefined){x.createdAt=persianDate();ch=true}if(x.price===undefined){x.price=null;ch=true}if(x.priceWords===undefined){x.priceWords=x.price!==null?numberToWords(x.price)+' تومان':'';ch=true}if(x.deliveryDate===undefined){x.deliveryDate='';ch=true}if(x.addDate===undefined){x.addDate=x.createdAt?(()=>{let m=String(x.createdAt).match(/(\d{4})\/(\d{1,2})\/(\d{1,2})/);return isoDate(new Date())})():isoDate(new Date());ch=true}if(ch)await put(x)}items=await all();setupDateInput('addDate');setupDateInput('deliveryDate');setupDateInput('editDate');render()}catch(e){document.getElementById('cards').innerHTML='<div class="empty">مرورگر شما ذخیره‌سازی سایت را فعال نکرده است. لطفاً با Chrome یا Edge باز کنید.</div>'}})();
</script></body></html>
