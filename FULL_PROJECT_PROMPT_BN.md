# Nahid Computer Website — Full Build Prompt

তুমি একজন অভিজ্ঞ Full-Stack Web Developer। “Nahid Computer” নামে একটি সম্পূর্ণ responsive, mobile-first ডিজিটাল সার্ভিস ওয়েবসাইট তৈরি/আপডেট করো। আগের কাজের ডিজাইন ও কার্যকর ফিচার বজায় রাখবে; অসম্পূর্ণ ফিচারকে সম্পূর্ণ বলে দাবি করবে না। GitHub Pages-ready ZIP দিতে হবে, সব ফাইল repository root-এ থাকবে এবং README বাংলায় হবে।

## ডিজাইন
- Dark navy, white, neon blue/cyan; আধুনিক digital vibe, smooth animation, responsive layout, clear buttons ও accessible forms।
- Welcome/Login-first অভিজ্ঞতা; Login-এর পর Customer Dashboard-এ top-right-এ Profile ও Logout। Admin একই Login পেজ থেকে প্রবেশ করবে, তবে Admin access Firebase UID-ভিত্তিক active admin record দিয়ে যাচাই হবে।
- সফলতার custom toast: “আহো ভাতিজা কাজ হয়ছে”; error toast এবং উপযুক্ত UI feedback।

## ব্যবসার তথ্য
- নাম: Nahid Computer।
- ঠিকানা: কোর্ট পাড়া, ২৯ নং দোকান, ফরিদপুর সদর, ফরিদপুর।
- ফোন/WhatsApp ও bKash Merchant নম্বর: বর্তমান কনফিগে দেওয়া ব্যবসার নম্বর; নতুন নম্বর অনুমান করে বানাবে না।
- সরকারি ফি বা অজানা মূল্য বানাবে না; মূল্য অজানা হলে “যোগাযোগ করে জানুন” দেখাবে।

## সার্ভিস ও প্রাথমিক মূল্য
- সাদা-কালো প্রিন্ট ৳১০/পৃষ্ঠা; কালার প্রিন্ট ৳২০/পৃষ্ঠা; স্ক্যান ৳২০/পৃষ্ঠা; পাসপোর্ট ছবি ৪ কপি ৳৫০।
- স্ট্যাম্প সার্ভিসে ৳১০০ স্ট্যাম্পের জন্য ৳১২০ (দোকানের উল্লেখিত চার্জসহ)।
- অনলাইন পর্চা ৳১৭০ + সহিমহরি ৳৫০০ (আগের তালিকায় উল্লেখিত; প্রকাশের আগে সঠিকতা যাচাইযোগ্যভাবে দেখাও)।
- খাজনা সার্ভিস ৳১০০; নামজারি সহায়তা ৳৫০০; TIN ৳২০০; Zero Return ৳৫০০; জন্মনিবন্ধন ও NID সংশোধনে সহায়তা ৳৩০০।
- ইনকাম ট্যাক্স রিটার্ন, এফিডেভিট, মর্টগেজ ডিড, ড্রাইভিং লার্নার, জমির পর্চা/খাজনা/মিউটেশন, প্রিন্ট/স্ক্যান/ফটোকপি ও অনলাইন আবেদন সহায়তা। Admin যেন service name, description, price, active status বদলাতে পারে।

## Authentication / Profile
- Firebase Authentication: Google Sign-in; ইমেইল verification বাধ্যতামূলক নয়; ফোন OTP আপাতত নয়।
- Profile-এ নাম ও মোবাইল নম্বর।
- Customer কেবল নিজের অর্ডার, পেমেন্ট, প্রোফাইল ও ফাইল দেখতে পারবে। Admin privilege client-side লুকানো বাটনের ওপর নির্ভর করবে না; Firestore Rules দিয়ে সুরক্ষিত হবে।

## Order System
- Service select, কাজের বিস্তারিত, fixed price অথবা quotation, optional files, unique Order ID, created time, order status।
- Status: Pending, Receive/Processing, Complete, Cancelled; Pending অর্ডার কাস্টমার বা Admin বাতিল করতে পারবে।
- Submit error handling, duplicate submission guard, Firebase permission error স্পষ্টভাবে দেখানো।

## Payment System — গুরুত্বপূর্ণ
- Order/Payment অংশে bKash স্টাইলের Payment card এবং “Pay Now” button থাকবে।
- Payment Link এখন খালি থাকবে; পরে Admin Panel থেকে HTTPS URL যোগ/পরিবর্তন/খালি করা যাবে।
- লিংক খালি থাকলে Pay Now বাটন disabled থাকবে; কোনো নকল বা অনুমান করা লিংক ব্যবহার করবে না।
- Admin Panel-এ Payment Link URL input ও Save button থাকবে। Firestore `siteSettings/payment`-এ সংরক্ষণ হবে; public read, admin-only write rules।
- পেমেন্ট শেষে Customer Transaction ID, যে মোবাইল নম্বর থেকে পেমেন্ট করেছে, এবং Amount জমা দেবে।
- Submit করলেই Paid হবে না; `Pending Verification` থাকবে। Admin নিজের bKash transaction history দেখে Confirm/Reject করবে। এটি manual verification, automatic gateway নয়।

## File Management
- Customer সর্বোচ্চ ১০ MB করে একাধিক ফাইল upload করবে; ফাইলের metadata ও order ID Firestore-এ থাকবে, bytes Firebase Storage-এ থাকবে।
- Admin customer-uploaded files দেখতে পারবে; Admin work files যোগ করবে; সঠিক customer নিজের dashboard থেকে দেখতে/download করতে পারবে।
- Customer File count শূন্য দেখানো, Admin Work File customer-এর কাছে না যাওয়া, broken storage paths, permission denied ও wrong order association—সব regression test করতে হবে।
- Storage ও Firestore Rules least-privilege হবে; অন্য customer-এর ফাইল access সম্ভব হবে না।

## Admin Panel
- Summary stats; order/customer/payment management; Receive/Complete/Cancel; file upload/download; service/price CRUD; Payment Link setting; AI knowledge base edit; notification management।
- Admin UID-এর `/admins/{uid}` document-এ `active: true` manually set হবে; clients নিজেরা admin grant করতে পারবে না।

## Notification & Invoice
- Dashboard notification এবং প্রয়োজন হলে email notification; order/payment/status/work-file update জানাবে।
- PDF/printable invoice-এ business info, order ID/date, customer, service, amount, payment status থাকবে।

## AI Customer Care
- বাংলা ও ইংরেজি chatbot; services, prices, address, contacts, common questions, order process/payment instructions সম্পর্কে উত্তর।
- Admin-editable knowledge base। Logged-in customer নিজের order সম্পর্কে জানতে পারবে; অন্য customer-এর তথ্য নয়।
- Free-tier API availability/quotas release-এর সময় যাচাই করবে। API key কখনো public frontend code-এ রাখবে না; Firebase Cloud Functions বা secure server secret ব্যবহার করবে। যদি backend নেই, স্পষ্টভাবে অসম্পূর্ণ setup হিসেবে চিহ্নিত করবে।

## Firebase / Deployment
- Existing Firebase project/config অকারণে বদলাবে না; project ID conflict থাকলে README-তে পরিষ্কার করে কোন config active তা চিহ্নিত করবে।
- Authentication, Firestore, Storage, security rules, `services`, `siteSettings`, `profiles`, `admins`, `orders`, payments/files data structures ঠিক করবে।
- GitHub Pages-ready root files: `index.html`, CSS/JS modules, Firebase config, `firestore.rules`, `storage.rules`, README-BN, setup status, `.nojekyll`।
- Firebase config-এর placeholder থাকলে clearly mark করবে। Service-account private key বা secret API key ZIP-এ রাখবে না।

## বাধ্যতামূলক পরীক্ষা
1. Mobile responsive + root index/style/script path।
2. Google login/logout/profile।
3. Customer order submit + reload-এ order দেখা।
4. Customer file upload → Admin visible।
5. Admin work file upload → only correct customer visible/download।
6. Payment Link empty → Pay Now disabled; Admin sets HTTPS link → button opens it; Admin clears link → disabled again।
7. Transaction ID + payer mobile + amount submission → Pending Verification; Admin confirm/reject।
8. Unauthorized user cannot access admin or another customer’s data/files.
9. AI key safety, errors, quota handling, README setup steps।
10. Final ZIP তৈরি, ZIP contents verify, setup limitations list।

কোডে বাস্তবে implement/test না করা feature-কে completed বলবে না। Final answer-এ ZIP download link, prompt, Firebase setup status এবং known limitations জানাবে।
