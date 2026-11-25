```react
import React, { useState, useEffect, useRef } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from 'firebase/auth';
import { getFirestore, doc, setDoc, addDoc, updateDoc, deleteDoc, onSnapshot, collection } from 'firebase/firestore';
import {
  Users, Wallet, HandCoins, FileText, Settings, Bell, LogOut, Plus, Edit3,
  Trash2, CheckCircle, XCircle, ShieldCheck, Smartphone, KeyRound, Upload,
  CreditCard, TrendingUp, TrendingDown, Award, Eye, Printer, Menu, X,
  Building2, Target, Send, UserPlus, Check, AlertCircle, RefreshCw, Sparkles
} from 'lucide-react';

// ============================================================================
// FIREBASE INITIALIZATION
// ============================================================================
const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {
  apiKey: "demo-key",
  authDomain: "demo.firebaseapp.com",
  projectId: "demo-project"
};
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'somiti-management-app';

// ============================================================================
// HELPER UTILITIES (BENGALI DIGITS, IMAGE COMPRESSION, CONSTANTS)
// ============================================================================
const toBn = (num) => {
  if (num === undefined || num === null) return '০';
  const bnDigits = ['০', '১', '২', '৩', '৪', '৫', '৬', '৭', '৮', '৯'];
  return num.toString().replace(/\d/g, (d) => bnDigits[d]);
};

const formatCurrency = (amount) => {
  const val = Number(amount) || 0;
  return `৳ ${toBn(val.toLocaleString('en-IN'))}`;
};

const MONTHS_BN = [
  'জানুয়ারি', 'ফেব্রুয়ারি', 'মার্চ', 'এপ্রিল', 'মে', 'জুন',
  'জুলাই', 'আগস্ট', 'সেপ্টেম্বর', 'অক্টোবর', 'নভেম্বর', 'ডিসেম্বর'
];

const YEARS_BN = ['২০২৪', '২০২৫', '২০২৬', '২০২৭', '২০২৮', '২০২৯', '২০৩০'];

const PAYMENT_METHODS = [
  { id: 'cash', name: 'নগদ / ক্যাশ (Cash)', color: 'bg-emerald-600' },
  { id: 'bkash', name: 'বিকাশ (bKash Online)', color: 'bg-pink-600' },
  { id: 'nagad', name: 'নগদ (Nagad Online)', color: 'bg-orange-600' },
  { id: 'rocket', name: 'রকেট (Rocket Online)', color: 'bg-purple-600' },
  { id: 'bank', name: 'ব্যাংক ট্রান্সফার (Bank)', color: 'bg-blue-600' }
];

const ROLE_LABELS = {
  main_admin: 'মেইন এডমিন (Main Admin)',
  admin: 'সহকারী এডমিন (Admin)',
  cashier: 'ক্যাশিয়ার (Cashier)',
  member: 'সাধারণ সদস্য (Member)'
};

// Compress image to Base64 so it safely fits in Firestore (<150KB)
const compressImageToBase64 = (file, maxWidth = 300, maxHeight = 300) => {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.readAsDataURL(file);
    reader.onload = (event) => {
      const img = new Image();
      img.src = event.target.result;
      img.onload = () => {
        const canvas = document.createElement('canvas');
        let width = img.width;
        let height = img.height;
        if (width > height) {
          if (width > maxWidth) {
            height *= maxWidth / width;
            width = maxWidth;
          }
        } else {
          if (height > maxHeight) {
            width *= maxHeight / height;
            height = maxHeight;
          }
        }
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext('2d');
        ctx.drawImage(img, 0, 0, width, height);
        resolve(canvas.toDataURL('image/jpeg', 0.75));
      };
      img.onerror = (err) => reject(err);
    };
    reader.onerror = (err) => reject(err);
  });
};

// ============================================================================
// DIGITAL SIGNATURE PAD COMPONENT
// ============================================================================
const SignaturePad = ({ value, onChange }) => {
  const canvasRef = useRef(null);
  const [isDrawing, setIsDrawing] = useState(false);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    ctx.strokeStyle = '#0f172a';
    ctx.lineWidth = 2.2;
    ctx.lineCap = 'round';
  }, []);

  const getCoords = (e) => {
    const canvas = canvasRef.current;
    const rect = canvas.getBoundingClientRect();
    const clientX = e.touches ? e.touches[0].clientX : e.clientX;
    const clientY = e.touches ? e.touches[0].clientY : e.clientY;
    return {
      x: (clientX - rect.left) * (canvas.width / rect.width),
      y: (clientY - rect.top) * (canvas.height / rect.height)
    };
  };

  const startDraw = (e) => {
    e.preventDefault();
    setIsDrawing(true);
    const { x, y } = getCoords(e);
    const ctx = canvasRef.current.getContext('2d');
    ctx.beginPath();
    ctx.moveTo(x, y);
  };

  const draw = (e) => {
    if (!isDrawing) return;
    e.preventDefault();
    const { x, y } = getCoords(e);
    const ctx = canvasRef.current.getContext('2d');
    ctx.lineTo(x, y);
    ctx.stroke();
  };

  const endDraw = () => {
    if (!isDrawing) return;
    setIsDrawing(false);
    const dataUrl = canvasRef.current.toDataURL('image/png');
    onChange(dataUrl);
  };

  const clearCanvas = () => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    onChange('');
  };

  const handleFileUpload = async (e) => {
    const file = e.target.files?.[0];
    if (file) {
      const base64 = await compressImageToBase64(file, 300, 120);
      onChange(base64);
    }
  };

  return (
    <div className="space-y-2">
      <div className="border-2 border-dashed border-slate-300 rounded-xl bg-slate-50 p-2 relative">
        <canvas
          ref={canvasRef}
          width={320}
          height={100}
          onMouseDown={startDraw}
          onMouseMove={draw}
          onMouseUp={endDraw}
          onMouseLeave={endDraw}
          onTouchStart={startDraw}
          onTouchMove={draw}
          onTouchEnd={endDraw}
          className="w-full h-24 bg-white rounded-lg cursor-crosshair touch-none border border-slate-200"
        />
        <div className="flex items-center justify-between mt-2 text-xs">
          <span className="text-slate-500">উপরে আঙুল বা মাউস দিয়ে স্বাক্ষর করুন অথবা ছবি আপলোড দিন</span>
          <div className="flex gap-2">
            <label className="cursor-pointer px-2.5 py-1 bg-slate-200 hover:bg-slate-300 text-slate-700 rounded-md font-medium transition">
              ছবি আপলোড
              <input type="file" accept="image/*" onChange={handleFileUpload} className="hidden" />
            </label>
            <button
              type="button"
              onClick={clearCanvas}
              className="px-2.5 py-1 bg-rose-100 hover:bg-rose-200 text-rose-700 rounded-md font-medium transition"
            >
              মুছুন
            </button>
          </div>
        </div>
      </div>
      {value && (
        <div className="flex items-center gap-3 p-2 bg-emerald-50 border border-emerald-200 rounded-lg">
          <span className="text-xs font-medium text-emerald-800">সংরক্ষিত স্বাক্ষর:</span>
          <img src={value} alt="Signature" className="h-10 object-contain bg-white px-2 py-1 rounded border" />
        </div>
      )}
    </div>
  );
};

// ============================================================================
// MAIN APPLICATION COMPONENT
// ============================================================================
export default function App() {
  // Firebase Auth User
  const [fbUser, setFbUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // App Session (Logged-in Society Member)
  const [currentUser, setCurrentUser] = useState(null);

  // Society Global Settings (Starts empty/default, editable anytime)
  const [settings, setSettings] = useState({
    societyName: 'আমার সমবায় সমিতি',
    tagline: 'একতা, সঞ্চয় ও সমৃদ্ধির পথে একসাথে',
    logoUrl: '',
    visionMission: 'আমাদের সমিতির মূল লক্ষ্য ও উদ্দেশ্য হলো সকল সদস্যের ক্ষুদ্র ক্ষুদ্র সঞ্চয় একত্রিত করে একটি শক্তিশালী তহবিল গঠন করা, সদস্যদের বিপদে-আপদে সহজ শর্তে ও স্বল্প লাভে ঋণ সহায়তা প্রদান করা এবং পারস্পরিক সহযোগিতার মাধ্যমে সবার অর্থনৈতিক ও সামাজিক উন্নয়ন নিশ্চিত করা।'
  });

  // Collections State (Starts 100% Empty / Zero)
  const [members, setMembers] = useState([]);
  const [transactions, setTransactions] = useState([]);
  const [loans, setLoans] = useState([]);
  const [notifications, setNotifications] = useState([]);

  // Navigation & UI State
  const [activeTab, setActiveTab] = useState('dashboard');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [toast, setToast] = useState(null);

  // Auth Screen States
  const [authMode, setAuthMode] = useState('signin'); // 'signin' | 'signup' | 'forgot'
  const [loginMobile, setLoginMobile] = useState('');
  const [loginPassword, setLoginPassword] = useState('');

  // Sign Up (Main Admin Initial Registration) States
  const [signupForm, setSignupForm] = useState({
    societyName: '',
    name: '',
    fatherName: '',
    motherName: '',
    spouseName: '',
    nomineeName: '',
    nid: '',
    mobile: '',
    password: ''
  });

  // OTP Forgot Password States
  const [otpStep, setOtpStep] = useState(1); // 1: Enter Mobile, 2: Verify OTP & New Password
  const [otpMobile, setOtpMobile] = useState('');
  const [generatedOtp, setGeneratedOtp] = useState('');
  const [enteredOtp, setEnteredOtp] = useState('');
  const [newResetPassword, setNewResetPassword] = useState('');

  // Modals State
  const [memberModalOpen, setMemberModalOpen] = useState(false);
  const [editingMember, setEditingMember] = useState(null);
  const [viewMemberDetails, setViewMemberDetails] = useState(null);
  const [receiptModalData, setReceiptModalData] = useState(null);
  const [loanModalOpen, setLoanModalOpen] = useState(false);

  // Member Form State
  const emptyMemberForm = {
    name: '',
    fatherName: '',
    motherName: '',
    spouseName: '',
    nomineeName: '',
    nid: '',
    mobile: '',
    password: '',
    role: 'member',
    photoUrl: '',
    signatureUrl: ''
  };
  const [memberForm, setMemberForm] = useState(emptyMemberForm);

  // Payment / Collection Form State
  const [paymentForm, setPaymentForm] = useState({
    memberId: '',
    type: 'subscription', // 'subscription' | 'installment'
    month: MONTHS_BN[new Date().getMonth()],
    year: '২০২৬',
    amount: '',
    method: 'cash',
    trxId: '',
    note: ''
  });

  // Income / Expense Form State
  const [ledgerForm, setLedgerForm] = useState({
    type: 'income', // 'income' | 'expense'
    title: '',
    amount: '',
    date: new Date().toISOString().split('T')[0],
    note: ''
  });

  // Loan Application Form State
  const [loanForm, setLoanForm] = useState({
    amount: '',
    installments: '12',
    purpose: ''
  });

  // Settings Edit Form State
  const [settingsForm, setSettingsForm] = useState(settings);

  // Show Custom Notification Toast
  const showToast = (message, type = 'success') => {
    setToast({ message, type });
    setTimeout(() => setToast(null), 5000);
  };

  // ==========================================================================
  // 1. FIREBASE AUTHENTICATION (RULE 3)
  // ==========================================================================
  useEffect(() => {
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (err) {
        console.error('Auth error:', err);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, (user) => {
      setFbUser(user);
      if (!user) setLoading(false);
    });
    return () => unsubscribe();
  }, []);

  // ==========================================================================
  // 2. FIRESTORE REALTIME LISTENERS (RULE 1 & RULE 2)
  // ==========================================================================
  useEffect(() => {
    if (!fbUser) return;

    // Listen to Society Settings
    const settingsDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'settings', 'main');
    const unsubSettings = onSnapshot(
      settingsDocRef,
      (snap) => {
        if (snap.exists()) {
          const data = snap.data();
          setSettings(data);
          setSettingsForm(data);
        }
      },
      (err) => console.error('Settings sync error:', err)
    );

    // Listen to Members
    const membersCol = collection(db, 'artifacts', appId, 'public', 'data', 'members');
    const unsubMembers = onSnapshot(
      membersCol,
      (snap) => {
        const list = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        list.sort((a, b) => (a.createdAt || 0) - (b.createdAt || 0));
        setMembers(list);

        // Keep current logged-in user synced if edited
        setCurrentUser((prev) => {
          if (!prev) return null;
          const updated = list.find((m) => m.id === prev.id);
          return updated || null;
        });

        // If no members exist yet, default auth screen to signup
        if (list.length === 0) {
          setAuthMode('signup');
        }
        setLoading(false);
      },
      (err) => {
        console.error('Members sync error:', err);
        setLoading(false);
      }
    );

    // Listen to Transactions (Subscriptions, Installments, Incomes, Expenses)
    const txCol = collection(db, 'artifacts', appId, 'public', 'data', 'transactions');
    const unsubTx = onSnapshot(
      txCol,
      (snap) => {
        const list = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        list.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
        setTransactions(list);
      },
      (err) => console.error('Transactions sync error:', err)
    );

    // Listen to Loans
    const loansCol = collection(db, 'artifacts', appId, 'public', 'data', 'loans');
    const unsubLoans = onSnapshot(
      loansCol,
      (snap) => {
        const list = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        list.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
        setLoans(list);
      },
      (err) => console.error('Loans sync error:', err)
    );

    // Listen to Cashier Notifications
    const notifCol = collection(db, 'artifacts', appId, 'public', 'data', 'notifications');
    const unsubNotif = onSnapshot(
      notifCol,
      (snap) => {
        const list = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        list.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));
        setNotifications(list);
      },
      (err) => console.error('Notifications sync error:', err)
    );

    return () => {
      unsubSettings();
      unsubMembers();
      unsubTx();
      unsubLoans();
      unsubNotif();
    };
  }, [fbUser]);

  // ==========================================================================
  // FINANCIAL CALCULATIONS (ALL START FROM ZERO ৳০)
  // ==========================================================================
  const totalSubscription = transactions
    .filter((t) => t.type === 'subscription')
    .reduce((sum, t) => sum + (Number(t.amount) || 0), 0);

  const totalInstallment = transactions
    .filter((t) => t.type === 'installment')
    .reduce((sum, t) => sum + (Number(t.amount) || 0), 0);

  const totalOtherIncome = transactions
    .filter((t) => t.type === 'income')
    .reduce((sum, t) => sum + (Number(t.amount) || 0), 0);

  const totalExpense = transactions
    .filter((t) => t.type === 'expense')
    .reduce((sum, t) => sum + (Number(t.amount) || 0), 0);

  const totalApprovedLoanDisbursed = loans
    .filter((l) => l.status === 'approved')
    .reduce((sum, l) => sum + (Number(l.amount) || 0), 0);

  const totalIncomeAll = totalSubscription + totalInstallment + totalOtherIncome;
  const currentBalance = totalIncomeAll - totalExpense - totalApprovedLoanDisbursed;

  // Role Checks
  const isMainAdmin = currentUser?.role === 'main_admin';
  const isAdmin = currentUser?.role === 'main_admin' || currentUser?.role === 'admin';
  const isCashier = currentUser?.role === 'cashier';

  const unreadCashierNotifs = notifications.filter((n) => !n.read).length;

  // ==========================================================================
  // AUTHENTICATION HANDLERS (SIGN UP, SIGN IN, OTP RESET)
  // ==========================================================================
  const handleMainAdminSignUp = async (e) => {
    e.preventDefault();
    if (!fbUser) return;

    if (members.length > 0) {
      showToast('মেইন এডমিন ইতিমধ্যে নিবন্ধিত আছেন! অনুগ্রহ করে সাইন ইন করুন।', 'error');
      setAuthMode('signin');
      return;
    }

    if (!signupForm.name.trim() || !signupForm.mobile.trim() || !signupForm.password.trim()) {
      showToast('নাম, মোবাইল নাম্বার এবং পাসওয়ার্ড অবশ্যই পূরণ করতে হবে।', 'error');
      return;
    }

    try {
      const chosenSocietyName = signupForm.societyName.trim() || 'আমার সমবায় সমিতি';
      const newSettings = {
        ...settings,
        societyName: chosenSocietyName
      };

      // Save initial society settings
      await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'settings', 'main'), newSettings);

      // Create Main Admin Member Record
      const adminData = {
        memberCode: 'SM-001',
        name: signupForm.name.trim(),
        fatherName: signupForm.fatherName.trim(),
        motherName: signupForm.motherName.trim(),
        spouseName: signupForm.spouseName.trim(),
        nomineeName: signupForm.nomineeName.trim(),
        nid: signupForm.nid.trim(),
        mobile: signupForm.mobile.trim(),
        password: signupForm.password.trim(),
        role: 'main_admin',
        photoUrl: '',
        signatureUrl: '',
        createdAt: Date.now()
      };

      const docRef = await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'members'), adminData);
      setCurrentUser({ id: docRef.id, ...adminData });
      showToast(`অভিনন্দন! "${chosenSocietyName}"-এর মেইন এডমিন হিসেবে আপনার অ্যাকাউন্ট তৈরি হয়েছে।`);
    } catch (err) {
      console.error(err);
      showToast('রেজিস্ট্রেশন করতে সমস্যা হয়েছে। আবার চেষ্টা করুন।', 'error');
    }
  };

  const handleSignIn = (e) => {
    e.preventDefault();
    if (members.length === 0) {
      showToast('এখনও কোনো সমিতি বা মেইন এডমিন তৈরি হয়নি। প্রথমে Sign Up করুন।', 'error');
      setAuthMode('signup');
      return;
    }

    const found = members.find(
      (m) => m.mobile.trim() === loginMobile.trim() && m.password === loginPassword
    );

    if (!found) {
      const mobileExists = members.some((m) => m.mobile.trim() === loginMobile.trim());
      if (!mobileExists) {
        showToast('এই মোবাইল নাম্বারটি নিবন্ধিত নয়! এডমিন আপনাকে যুক্ত করার পর সাইন ইন করতে পারবেন।', 'error');
      } else {
        showToast('পাসওয়ার্ড ভুল হয়েছে! সঠিক পাসওয়ার্ড দিন অথবা OTP দিয়ে রিসেট করুন।', 'error');
      }
      return;
    }

    setCurrentUser(found);
    setLoginMobile('');
    setLoginPassword('');
    showToast(`স্বাগতম, ${found.name}!`);
  };

  const handleSendOtp = (e) => {
    e.preventDefault();
    const userExists = members.find((m) => m.mobile.trim() === otpMobile.trim());
    if (!userExists) {
      showToast('এই মোবাইল নাম্বারে কোনো সদস্য নিবন্ধিত নেই!', 'error');
      return;
    }
    const code = Math.floor(100000 + Math.random() * 900000).toString();
    setGeneratedOtp(code);
    setOtpStep(2);
    showToast(`আপনার মোবাইল (${otpMobile})-এ ৬ ডিজিটের OTP কোড পাঠানো হয়েছে: ${code}`, 'info');
  };

  const handleVerifyOtpAndReset = async (e) => {
    e.preventDefault();
    if (enteredOtp.trim() !== generatedOtp) {
      showToast('OTP কোডটি সঠিক নয়! আবার যাচাই করুন।', 'error');
      return;
    }
    if (newResetPassword.trim().length < 4) {
      showToast('নতুন পাসওয়ার্ড কমপক্ষে ৪ অক্ষরের হতে হবে।', 'error');
      return;
    }

    try {
      const targetUser = members.find((m) => m.mobile.trim() === otpMobile.trim());
      if (targetUser) {
        await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'members', targetUser.id), {
          password: newResetPassword.trim()
        });
        showToast('পাসওয়ার্ড সফলভাবে পরিবর্তন হয়েছে! এখন নতুন পাসওয়ার্ড দিয়ে লগইন করুন।');
        setAuthMode('signin');
        setOtpStep(1);
        setOtpMobile('');
        setEnteredOtp('');
        setNewResetPassword('');
        setGeneratedOtp('');
      }
    } catch (err) {
      console.error(err);
      showToast('পাসওয়ার্ড রিসেট করতে সমস্যা হয়েছে।', 'error');
    }
  };

  // ==========================================================================
  // MEMBER CRUD HANDLERS (ADD / EDIT BY ADMIN)
  // ==========================================================================
  const openAddMemberModal = () => {
    setEditingMember(null);
    setMemberForm(emptyMemberForm);
    setMemberModalOpen(true);
  };

  const openEditMemberModal = (member) => {
    setEditingMember(member);
    setMemberForm({
      name: member.name || '',
      fatherName: member.fatherName || '',
      motherName: member.motherName || '',
      spouseName: member.spouseName || '',
      nomineeName: member.nomineeName || '',
      nid: member.nid || '',
      mobile: member.mobile || '',
      password: member.password || '',
      role: member.role || 'member',
      photoUrl: member.photoUrl || '',
      signatureUrl: member.signatureUrl || ''
    });
    setMemberModalOpen(true);
  };

  const handlePhotoUpload = async (e) => {
    const file = e.target.files?.[0];
    if (file) {
      const compressed = await compressImageToBase64(file, 300, 300);
      setMemberForm((prev) => ({ ...prev, photoUrl: compressed }));
    }
  };

  const handleSaveMember = async (e) => {
    e.preventDefault();
    if (!fbUser || !isAdmin) return;

    if (!memberForm.name.trim() || !memberForm.mobile.trim() || !memberForm.password.trim()) {
      showToast('সদস্যের নাম, মোবাইল নাম্বার এবং লগইন পাসওয়ার্ড অবশ্যই দিতে হবে।', 'error');
      return;
    }

    // Check duplicate mobile number
    const duplicate = members.find(
      (m) => m.mobile.trim() === memberForm.mobile.trim() && m.id !== editingMember?.id
    );
    if (duplicate) {
      showToast('এই মোবাইল নাম্বারটি ইতিমধ্যে অন্য সদস্যের জন্য ব্যবহৃত হয়েছে!', 'error');
      return;
    }

    try {
      if (editingMember) {
        // Prevent demoting the sole main_admin accidentally
        const finalRole =
          editingMember.role === 'main_admin' && !isMainAdmin ? 'main_admin' : memberForm.role;

        await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'members', editingMember.id), {
          ...memberForm,
          role: finalRole,
          mobile: memberForm.mobile.trim(),
          name: memberForm.name.trim()
        });
        showToast(`${memberForm.name}-এর সকল তথ্য সফলভাবে আপডেট করা হয়েছে।`);
      } else {
        const nextCode = `SM-${String(members.length + 1).padStart(3, '0')}`;
        await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'members'), {
          ...memberForm,
          memberCode: nextCode,
          mobile: memberForm.mobile.trim(),
          name: memberForm.name.trim(),
          createdAt: Date.now()
        });
        showToast(`নতুন সদস্য "${memberForm.name}" যুক্ত হয়েছেন! এখন তিনি মোবাইল নাম্বার ও পাসওয়ার্ড দিয়ে লগইন করতে পারবেন।`);
      }
      setMemberModalOpen(false);
      setEditingMember(null);
      setMemberForm(emptyMemberForm);
    } catch (err) {
      console.error(err);
      showToast('তথ্য সংরক্ষণ করতে সমস্যা হয়েছে।', 'error');
    }
  };

  const handleDeleteMember = async (member) => {
    if (!isMainAdmin) {
      showToast('শুধুমাত্র মেইন এডমিন সদস্য ডিলিট করতে পারবেন।', 'error');
      return;
    }
    if (member.role === 'main_admin') {
      showToast('মেইন এডমিন অ্যাকাউন্ট ডিলিট করা যাবে না।', 'error');
      return;
    }
    try {
      await deleteDoc(doc(db, 'artifacts', appId, 'public', 'data', 'members', member.id));
      showToast(`${member.name}-কে তালিকা থেকে মুছে ফেলা হয়েছে।`);
    } catch (err) {
      console.error(err);
      showToast('সদস্য মুছতে সমস্যা হয়েছে।', 'error');
    }
  };

  // ==========================================================================
  // PAYMENT & COLLECTION HANDLER (SUBSCRIPTION / INSTALLMENT / ONLINE)
  // ==========================================================================
  const handlePaymentSubmit = async (e) => {
    e.preventDefault();
    if (!fbUser) return;

    const targetMemberId = isAdmin || isCashier ? paymentForm.memberId || currentUser.id : currentUser.id;
    const targetMember = members.find((m) => m.id === targetMemberId);

    if (!targetMember) {
      showToast('অনুগ্রহ করে সদস্য নির্বাচন করুন।', 'error');
      return;
    }

    const amt = Number(paymentForm.amount);
    if (!amt || amt <= 0) {
      showToast('সঠিক টাকার পরিমাণ লিখুন।', 'error');
      return;
    }

    if (paymentForm.method !== 'cash' && !paymentForm.trxId.trim()) {
      showToast('অনলাইন পেমেন্টের ক্ষেত্রে Transaction ID / রেফারেন্স নাম্বার দিন।', 'error');
      return;
    }

    try {
      const receiptNo = `REC-${Date.now().toString().slice(-6)}`;
      const methodObj = PAYMENT_METHODS.find((m) => m.id === paymentForm.method);

      const txData = {
        receiptNo,
        memberId: targetMember.id,
        memberName: targetMember.name,
        memberCode: targetMember.memberCode || '',
        memberMobile: targetMember.mobile,
        type: paymentForm.type, // 'subscription' | 'installment'
        month: paymentForm.month,
        year: paymentForm.year,
        amount: amt,
        method: paymentForm.method,
        methodName: methodObj ? methodObj.name : paymentForm.method,
        trxId: paymentForm.trxId.trim() || 'CASH',
        note: paymentForm.note.trim(),
        collectedBy: currentUser.name,
        date: new Date().toISOString().split('T')[0],
        createdAt: Date.now()
      };

      const docRef = await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'transactions'), txData);
      setReceiptModalData({ id: docRef.id, ...txData });
      setPaymentForm({
        ...paymentForm,
        amount: '',
        trxId: '',
        note: ''
      });
      showToast('পেমেন্ট সফলভাবে সম্পন্ন হয়েছে এবং রশিদ তৈরি হয়েছে!');
    } catch (err) {
      console.error(err);
      showToast('পেমেন্ট সংরক্ষণ করতে সমস্যা হয়েছে।', 'error');
    }
  };

  // ==========================================================================
  // INCOME & EXPENSE LEDGER HANDLER
  // ==========================================================================
  const handleLedgerSubmit = async (e) => {
    e.preventDefault();
    if (!fbUser || (!isAdmin && !isCashier)) return;

    const amt = Number(ledgerForm.amount);
    if (!ledgerForm.title.trim() || !amt || amt <= 0) {
      showToast('খাতের বিবরণ এবং সঠিক টাকার পরিমাণ দিন।', 'error');
      return;
    }

    try {
      await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'transactions'), {
        receiptNo: `TRX-${Date.now().toString().slice(-6)}`,
        type: ledgerForm.type, // 'income' | 'expense'
        title: ledgerForm.title.trim(),
        memberName: ledgerForm.title.trim(),
        amount: amt,
        date: ledgerForm.date,
        note: ledgerForm.note.trim(),
        collectedBy: currentUser.name,
        createdAt: Date.now()
      });
      setLedgerForm({
        type: 'income',
        title: '',
        amount: '',
        date: new Date().toISOString().split('T')[0],
        note: ''
      });
      showToast(ledgerForm.type === 'income' ? 'অন্যান্য আয় যুক্ত হয়েছে।' : 'ব্যয়ের হিসাব যুক্ত হয়েছে।');
    } catch (err) {
      console.error(err);
      showToast('হিসাব সংরক্ষণ করতে সমস্যা হয়েছে।', 'error');
    }
  };

  // ==========================================================================
  // LOAN APPLICATION & ADMIN APPROVAL -> CASHIER NOTIFICATION
  // ==========================================================================
  const handleLoanApply = async (e) => {
    e.preventDefault();
    if (!fbUser) return;

    const amt = Number(loanForm.amount);
    if (!amt || amt <= 0 || !loanForm.purpose.trim()) {
      showToast('লোনের পরিমাণ এবং কারণ সঠিকভাবে উল্লেখ করুন।', 'error');
      return;
    }

    try {
      await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'loans'), {
        memberId: currentUser.id,
        memberName: currentUser.name,
        memberCode: currentUser.memberCode || '',
        memberMobile: currentUser.mobile,
        amount: amt,
        installments: Number(loanForm.installments) || 12,
        purpose: loanForm.purpose.trim(),
        status: 'pending', // 'pending' | 'approved' | 'rejected'
        appliedDate: new Date().toISOString().split('T')[0],
        createdAt: Date.now()
      });
      setLoanForm({ amount: '', installments: '12', purpose: '' });
      setLoanModalOpen(false);
      showToast('আপনার লোনের আবেদন সফলভাবে জমা হয়েছে! এডমিন অনুমোদনের পর ক্যাশিয়ারকে জানানো হবে।');
    } catch (err) {
      console.error(err);
      showToast('লোনের আবেদন জমা দিতে সমস্যা হয়েছে।', 'error');
    }
  };

  const handleLoanDecision = async (loan, decision) => {
    if (!fbUser || !isAdmin) return;

    try {
      await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'loans', loan.id), {
        status: decision,
        approvedBy: currentUser.name,
        decisionDate: new Date().toISOString().split('T')[0]
      });

      // If APPROVED, automatically send message/notification to Cashier!
      if (decision === 'approved') {
        const cashierMember = members.find((m) => m.role === 'cashier');
        const cashierName = cashierMember ? cashierMember.name : 'ক্যাশিয়ার';

        await addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'notifications'), {
          toRole: 'cashier',
          cashierName,
          loanId: loan.id,
          memberName: loan.memberName,
          memberMobile: loan.memberMobile,
          amount: loan.amount,
          installments: loan.installments,
          approvedBy: currentUser.name,
          message: `জরুরি বার্তা (${cashierName}): সদস্য "${loan.memberName}" (মোবাইল: ${loan.memberMobile})-এর ${formatCurrency(loan.amount)} টাকার লোন আবেদন এডমিন (${currentUser.name}) কর্তৃক অনুমোদিত হয়েছে। অনুগ্রহ করে তহবিল থেকে লোনটি বিতরণের ব্যবস্থা নিন।`,
          read: false,
          createdAt: Date.now()
        });

        showToast(`লোন অনুমোদিত হয়েছে এবং ক্যাশিয়ার (${cashierName})-এর নিকট অটোমেটিক মেসেজ পাঠানো হয়েছে!`);
      } else {
        showToast('লোনের আবেদন বাতিল করা হয়েছে।', 'info');
      }
    } catch (err) {
      console.error(err);
      showToast('সিদ্ধান্ত আপডেট করতে সমস্যা হয়েছে।', 'error');
    }
  };

  const markAllNotificationsRead = async () => {
    try {
      const unread = notifications.filter((n) => !n.read);
      for (const n of unread) {
        await updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'notifications', n.id), {
          read: true
        });
      }
      showToast('সকল নোটিফিকেশন পঠিত হিসেবে চিহ্নিত হয়েছে।');
    } catch (err) {
      console.error(err);
    }
  };

  // ==========================================================================
  // SETTINGS UPDATE (SOCIETY NAME, LOGO, VISION & MISSION)
  // ==========================================================================
  const handleLogoUpload = async (e) => {
    const file = e.target.files?.[0];
    if (file) {
      const compressed = await compressImageToBase64(file, 250, 250);
      setSettingsForm((prev) => ({ ...prev, logoUrl: compressed }));
    }
  };

  const handleSaveSettings = async (e) => {
    e.preventDefault();
    if (!fbUser || !isAdmin) return;

    try {
      await setDoc(doc(db, 'artifacts', appId, 'public', 'data', 'settings', 'main'), {
        ...settingsForm,
        societyName: settingsForm.societyName.trim() || 'আমার সমবায় সমিতি'
      });
      showToast('সমিতির নাম, লোগো ও লক্ষ্য-উদ্দেশ্য সফলভাবে আপডেট হয়েছে!');
    } catch (err) {
      console.error(err);
      showToast('সেটিংস সংরক্ষণ করতে সমস্যা হয়েছে।', 'error');
    }
  };

  // ==========================================================================
  // LOADING SCREEN
  // ==========================================================================
  if (loading) {
    return (
      <div className="min-h-screen bg-slate-900 flex flex-col items-center justify-center text-white p-4">
        <div className="w-12 h-12 border-4 border-emerald-400 border-t-transparent rounded-full animate-spin mb-4"></div>
        <p className="text-lg font-medium text-emerald-300">সমিতি অ্যাপ লোড হচ্ছে...</p>
      </div>
    );
  }

  // ==========================================================================
  // AUTHENTICATION PORTAL (WHEN NOT LOGGED IN)
  // ==========================================================================
  if (!currentUser) {
    return (
      <div className="min-h-screen bg-gradient-to-br from-emerald-950 via-slate-900 to-emerald-900 flex flex-col justify-center items-center p-4">
        {/* Global Toast */}
        {toast && (
          <div className={`fixed top-4 right-4 z-50 max-w-md px-4 py-3 rounded-xl shadow-2xl border flex items-center gap-3 animate-bounce ${
            toast.type === 'error' ? 'bg-rose-900/95 border-rose-500 text-white' :
            toast.type === 'info' ? 'bg-amber-900/95 border-amber-400 text-white' :
            'bg-emerald-900/95 border-emerald-400 text-white'
          }`}>
            <AlertCircle className="w-5 h-5 shrink-0" />
            <p className="text-sm font-medium">{toast.message}</p>
          </div>
        )}

        <div className="w-full max-w-lg bg-white rounded-3xl shadow-2xl overflow-hidden border border-emerald-500/20">
          {/* Header Branding */}
          <div className="bg-gradient-to-r from-emerald-700 to-teal-700 p-6 text-center text-white relative">
            <div className="w-16 h-16 mx-auto bg-white/15 backdrop-blur rounded-2xl flex items-center justify-center mb-3 border border-white/25 overflow-hidden">
              {settings.logoUrl ? (
                <img src={settings.logoUrl} alt="Logo" className="w-full h-full object-cover" />
              ) : (
                <Building2 className="w-9 h-9 text-emerald-200" />
              )}
            </div>
            <h1 className="text-2xl font-bold tracking-tight">{settings.societyName}</h1>
            <p className="text-emerald-100 text-xs mt-1">{settings.tagline}</p>
          </div>

          {/* Auth Mode Tabs */}
          <div className="flex border-b border-slate-200 bg-slate-50">
            <button
              onClick={() => setAuthMode('signin')}
              className={`flex-1 py-3.5 text-sm font-semibold transition ${
                authMode === 'signin'
                  ? 'bg-white text-emerald-700 border-b-2 border-emerald-600'
                  : 'text-slate-500 hover:text-slate-700'
              }`}
            >
              সাইন ইন (Sign In)
            </button>
            {members.length === 0 && (
              <button
                onClick={() => setAuthMode('signup')}
                className={`flex-1 py-3.5 text-sm font-semibold transition ${
                  authMode === 'signup'
                    ? 'bg-white text-emerald-700 border-b-2 border-emerald-600'
                    : 'text-slate-500 hover:text-slate-700'
                }`}
              >
                নতুন সমিতি শুরু করুন (Sign Up)
              </button>
            )}
            <button
              onClick={() => { setAuthMode('forgot'); setOtpStep(1); }}
              className={`flex-1 py-3.5 text-sm font-semibold transition ${
                authMode === 'forgot'
                  ? 'bg-white text-emerald-700 border-b-2 border-emerald-600'
                  : 'text-slate-500 hover:text-slate-700'
              }`}
            >
              পাসওয়ার্ড রিসেট (OTP)
            </button>
          </div>

          <div className="p-6 sm:p-8">
            {/* 1. SIGN IN FORM */}
            {authMode === 'signin' && (
              <form onSubmit={handleSignIn} className="space-y-4">
                {members.length === 0 ? (
                  <div className="p-4 bg-amber-50 border border-amber-200 rounded-xl text-amber-800 text-sm space-y-2">
                    <p className="font-semibold">এখনও কোনো সমিতি তৈরি করা হয়নি!</p>
                    <p>আপনি যদি নতুন সমিতি শুরু করতে চান, তবে উপরের <b>"নতুন সমিতি শুরু করুন (Sign Up)"</b> ট্যাবে ক্লিক করে মেইন এডমিন হিসেবে রেজিস্ট্রেশন করুন।</p>
                  </div>
                ) : (
                  <div className="p-3 bg-emerald-50 border border-emerald-200 rounded-xl text-emerald-800 text-xs">
                    এডমিন কর্তৃক আপনার তথ্য ও মোবাইল নাম্বার সেটআপ করার পর নিচে মোবাইল নাম্বার ও পাসওয়ার্ড দিয়ে লগইন করুন।
                  </div>
                )}

                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-1">মোবাইল নাম্বার</label>
                  <div className="relative">
                    <Smartphone className="w-5 h-5 text-slate-400 absolute left-3 top-3" />
                    <input
                      type="text"
                      required
                      placeholder="01XXXXXXXXX"
                      value={loginMobile}
                      onChange={(e) => setLoginMobile(e.target.value)}
                      className="w-full pl-10 pr-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none"
                    />
                  </div>
                </div>

                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-1">পাসওয়ার্ড</label>
                  <div className="relative">
                    <KeyRound className="w-5 h-5 text-slate-400 absolute left-3 top-3" />
                    <input
                      type="password"
                      required
                      placeholder="আপনার পাসওয়ার্ড দিন"
                      value={loginPassword}
                      onChange={(e) => setLoginPassword(e.target.value)}
                      className="w-full pl-10 pr-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none"
                    />
                  </div>
                </div>

                <div className="flex justify-end">
                  <button
                    type="button"
                    onClick={() => { setAuthMode('forgot'); setOtpStep(1); }}
                    className="text-xs font-semibold text-emerald-700 hover:underline"
                  >
                    পাসওয়ার্ড ভুলে গেছেন? মোবাইল OTP দিয়ে রিসেট করুন
                  </button>
                </div>

                <button
                  type="submit"
                  className="w-full py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg shadow-emerald-600/30 transition"
                >
                  সাইন ইন করুন
                </button>
              </form>
            )}

            {/* 2. SIGN UP FORM (FIRST USER = MAIN ADMIN) */}
            {authMode === 'signup' && members.length === 0 && (
              <form onSubmit={handleMainAdminSignUp} className="space-y-3.5">
                <div className="p-3 bg-blue-50 border border-blue-200 rounded-xl text-blue-800 text-xs">
                  <b>প্রথম নিবন্ধনকারী হিসেবে আপনি "মেইন এডমিন" হবেন।</b> পরবর্তীতে আপনি অ্যাপের নাম, লোগো, লক্ষ্য-উদ্দেশ্য পরিবর্তন এবং অন্যান্য সদস্য ও এডমিন যুক্ত করতে পারবেন। সব হিসাব <b>৳০ (শূন্য)</b> থেকে শুরু হবে।
                </div>

                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">আপনার সমিতির নাম (পরেও পরিবর্তন করা যাবে)</label>
                  <input
                    type="text"
                    placeholder="যেমন: আদর্শ সঞ্চয় ও ঋণদান সমবায় সমিতি"
                    value={signupForm.societyName}
                    onChange={(e) => setSignupForm({ ...signupForm, societyName: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                  />
                </div>

                <div className="grid grid-cols-1 sm:grid-cols-2 gap-3">
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">আপনার পূর্ণ নাম (মেইন এডমিন) *</label>
                    <input
                      type="text"
                      required
                      placeholder="পূর্ণ নাম লিখুন"
                      value={signupForm.name}
                      onChange={(e) => setSignupForm({ ...signupForm, name: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">মোবাইল নাম্বার (লগইন আইডি) *</label>
                    <input
                      type="text"
                      required
                      placeholder="01XXXXXXXXX"
                      value={signupForm.mobile}
                      onChange={(e) => setSignupForm({ ...signupForm, mobile: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                </div>

                <div className="grid grid-cols-1 sm:grid-cols-2 gap-3">
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">পিতার নাম</label>
                    <input
                      type="text"
                      placeholder="পিতার নাম"
                      value={signupForm.fatherName}
                      onChange={(e) => setSignupForm({ ...signupForm, fatherName: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">মাতার নাম</label>
                    <input
                      type="text"
                      placeholder="মাতার নাম"
                      value={signupForm.motherName}
                      onChange={(e) => setSignupForm({ ...signupForm, motherName: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                </div>

                <div className="grid grid-cols-1 sm:grid-cols-2 gap-3">
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">জাতীয় পরিচয়পত্র (NID)</label>
                    <input
                      type="text"
                      placeholder="NID নম্বর"
                      value={signupForm.nid}
                      onChange={(e) => setSignupForm({ ...signupForm, nid: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                  <div>
                    <label className="block text-xs font-bold text-slate-700 mb-1">নমিনির নাম</label>
                    <input
                      type="text"
                      placeholder="নমিনির নাম"
                      value={signupForm.nomineeName}
                      onChange={(e) => setSignupForm({ ...signupForm, nomineeName: e.target.value })}
                      className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                    />
                  </div>
                </div>

                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">পাসওয়ার্ড সেট করুন *</label>
                  <input
                    type="password"
                    required
                    placeholder="নতুন পাসওয়ার্ড দিন"
                    value={signupForm.password}
                    onChange={(e) => setSignupForm({ ...signupForm, password: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-emerald-500 outline-none"
                  />
                </div>

                <button
                  type="submit"
                  className="w-full py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg transition mt-2"
                >
                  মেইন এডমিন হিসেবে সমিতি চালু করুন
                </button>
              </form>
            )}

            {/* 3. FORGOT PASSWORD WITH MOBILE OTP */}
            {authMode === 'forgot' && (
              <div className="space-y-4">
                <div className="p-3 bg-amber-50 border border-amber-200 rounded-xl text-amber-900 text-xs">
                  আপনার নিবন্ধিত মোবাইল নাম্বারটি লিখুন। মোবাইলে ৬ ডিজিটের একটি OTP কোড পাঠানো হবে, যা দিয়ে আপনি নতুন পাসওয়ার্ড সেট করতে পারবেন।
                </div>

                {otpStep === 1 ? (
                  <form onSubmit={handleSendOtp} className="space-y-4">
                    <div>
                      <label className="block text-sm font-semibold text-slate-700 mb-1">নিবন্ধিত মোবাইল নাম্বার</label>
                      <input
                        type="text"
                        required
                        placeholder="01XXXXXXXXX"
                        value={otpMobile}
                        onChange={(e) => setOtpMobile(e.target.value)}
                        className="w-full px-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none"
                      />
                    </div>
                    <button
                      type="submit"
                      className="w-full py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl transition"
                    >
                      মোবাইলে OTP পাঠান
                    </button>
                  </form>
                ) : (
                  <form onSubmit={handleVerifyOtpAndReset} className="space-y-4">
                    <div className="p-3 bg-emerald-100 border border-emerald-300 rounded-xl text-emerald-900 text-center">
                      <p className="text-xs">আপনার মোবাইলে প্রেরিত OTP কোড:</p>
                      <p className="text-xl font-extrabold tracking-widest mt-1">{generatedOtp}</p>
                    </div>

                    <div>
                      <label className="block text-sm font-semibold text-slate-700 mb-1">৬ ডিজিটের OTP কোড লিখুন</label>
                      <input
                        type="text"
                        required
                        placeholder="XXXXXX"
                        value={enteredOtp}
                        onChange={(e) => setEnteredOtp(e.target.value)}
                        className="w-full px-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none text-center font-bold tracking-widest"
                      />
                    </div>

                    <div>
                      <label className="block text-sm font-semibold text-slate-700 mb-1">নতুন পাসওয়ার্ড দিন</label>
                      <input
                        type="password"
                        required
                        placeholder="নতুন পাসওয়ার্ড"
                        value={newResetPassword}
                        onChange={(e) => setNewResetPassword(e.target.value)}
                        className="w-full px-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none"
                      />
                    </div>

                    <div className="flex gap-2">
                      <button
                        type="button"
                        onClick={() => setOtpStep(1)}
                        className="flex-1 py-2.5 bg-slate-200 hover:bg-slate-300 text-slate-700 font-semibold rounded-xl"
                      >
                        পিছনে যান
                      </button>
                      <button
                        type="submit"
                        className="flex-2 py-2.5 px-6 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl"
                      >
                        পাসওয়ার্ড পরিবর্তন করুন
                      </button>
                    </div>
                  </form>
                )}
              </div>
            )}
          </div>
        </div>
      </div>
    );
  }

  // ==========================================================================
  // LOGGED-IN MAIN DASHBOARD LAYOUT
  // ==========================================================================
  const navItems = [
    { id: 'dashboard', label: 'ড্যাশবোর্ড ও লক্ষ্য', icon: Target },
    { id: 'members', label: 'সদস্য ও এডমিন তালিকা', icon: Users },
    { id: 'payments', label: 'চাঁদা ও কিস্তি (Online)', icon: CreditCard },
    { id: 'ledger', label: 'আয়-ব্যয়ের হিসাব', icon: FileText },
    { id: 'loans', label: 'লোন আবেদন ও অনুমোদন', icon: HandCoins },
    { id: 'notifications', label: 'ক্যাশিয়ার মেসেজ বক্স', icon: Bell, badge: unreadCashierNotifs },
    ...(isAdmin ? [{ id: 'settings', label: 'সমিতি সেটিংস (নাম/লোগো)', icon: Settings }] : [])
  ];

  return (
    <div className="min-h-screen bg-slate-100 flex flex-col md:flex-row text-slate-800">
      {/* Global Toast */}
      {toast && (
        <div className={`fixed top-4 right-4 z-50 max-w-md px-4 py-3 rounded-xl shadow-2xl border flex items-center gap-3 ${
          toast.type === 'error' ? 'bg-rose-900 border-rose-500 text-white' :
          toast.type === 'info' ? 'bg-amber-900 border-amber-400 text-white' :
          'bg-emerald-900 border-emerald-400 text-white'
        }`}>
          <CheckCircle className="w-5 h-5 shrink-0 text-emerald-300" />
          <p className="text-sm font-medium">{toast.message}</p>
        </div>
      )}

      {/* SIDEBAR NAVIGATION (DESKTOP) */}
      <aside className="hidden md:flex md:w-72 bg-slate-900 text-white flex-col justify-between shrink-0 shadow-xl">
        <div>
          {/* Editable Society Brand Header */}
          <div className="p-5 border-b border-slate-800 flex items-center gap-3">
            <div className="w-12 h-12 rounded-2xl bg-emerald-600/20 border border-emerald-500/40 flex items-center justify-center overflow-hidden shrink-0">
              {settings.logoUrl ? (
                <img src={settings.logoUrl} alt="Logo" className="w-full h-full object-cover" />
              ) : (
                <Building2 className="w-7 h-7 text-emerald-400" />
              )}
            </div>
            <div className="min-w-0 flex-1">
              <div className="flex items-center gap-1.5">
                <h2 className="font-bold text-base truncate text-white">{settings.societyName}</h2>
                {isAdmin && (
                  <button
                    onClick={() => setActiveTab('settings')}
                    title="সমিতির নাম ও লোগো এডিট করুন"
                    className="text-emerald-400 hover:text-emerald-300"
                  >
                    <Edit3 className="w-3.5 h-3.5" />
                  </button>
                )}
              </div>
              <p className="text-xs text-slate-400 truncate">{settings.tagline}</p>
            </div>
          </div>

          {/* Navigation Menu */}
          <nav className="p-3 space-y-1">
            {navItems.map((item) => {
              const Icon = item.icon;
              const active = activeTab === item.id;
              return (
                <button
                  key={item.id}
                  onClick={() => setActiveTab(item.id)}
                  className={`w-full flex items-center justify-between px-4 py-3 rounded-xl text-sm font-medium transition ${
                    active
                      ? 'bg-emerald-600 text-white shadow-lg shadow-emerald-600/25'
                      : 'text-slate-300 hover:bg-slate-800 hover:text-white'
                  }`}
                >
                  <span className="flex items-center gap-3">
                    <Icon className="w-5 h-5" />
                    {item.label}
                  </span>
                  {item.badge > 0 && (
                    <span className="px-2 py-0.5 text-xs font-bold bg-rose-500 text-white rounded-full">
                      {toBn(item.badge)}
                    </span>
                  )}
                </button>
              );
            })}
          </nav>
        </div>

        {/* Logged-in User Footer Card */}
        <div className="p-4 border-t border-slate-800 bg-slate-950/50">
          <div className="flex items-center gap-3 mb-3">
            <div className="w-10 h-10 rounded-full bg-emerald-700 flex items-center justify-center font-bold text-white overflow-hidden border border-emerald-400/40 shrink-0">
              {currentUser.photoUrl ? (
                <img src={currentUser.photoUrl} alt={currentUser.name} className="w-full h-full object-cover" />
              ) : (
                currentUser.name.charAt(0)
              )}
            </div>
            <div className="min-w-0 flex-1">
              <p className="text-sm font-bold text-white truncate">{currentUser.name}</p>
              <p className="text-xs text-emerald-400 truncate">{ROLE_LABELS[currentUser.role]}</p>
            </div>
          </div>
          <button
            onClick={() => setCurrentUser(null)}
            className="w-full py-2 px-3 bg-rose-600/20 hover:bg-rose-600 text-rose-300 hover:text-white rounded-xl text-xs font-semibold flex items-center justify-center gap-2 transition"
          >
            <LogOut className="w-4 h-4" /> লগ আউট করুন
          </button>
        </div>
      </aside>

      {/* MOBILE TOP BAR */}
      <header className="md:hidden bg-slate-900 text-white px-4 py-3 flex items-center justify-between sticky top-0 z-30 shadow-md">
        <div className="flex items-center gap-2.5 min-w-0">
          <div className="w-9 h-9 rounded-xl bg-emerald-600/30 flex items-center justify-center overflow-hidden shrink-0">
            {settings.logoUrl ? (
              <img src={settings.logoUrl} alt="Logo" className="w-full h-full object-cover" />
            ) : (
              <Building2 className="w-5 h-5 text-emerald-400" />
            )}
          </div>
          <div className="truncate">
            <h1 className="font-bold text-sm truncate">{settings.societyName}</h1>
            <p className="text-[11px] text-emerald-400">{currentUser.name}</p>
          </div>
        </div>
        <div className="flex items-center gap-2">
          <button
            onClick={() => setActiveTab('notifications')}
            className="relative p-2 bg-slate-800 rounded-lg text-slate-200"
          >
            <Bell className="w-5 h-5" />
            {unreadCashierNotifs > 0 && (
              <span className="absolute -top-1 -right-1 w-4 h-4 bg-rose-500 text-[10px] font-bold rounded-full flex items-center justify-center">
                {toBn(unreadCashierNotifs)}
              </span>
            )}
          </button>
          <button
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
            className="p-2 bg-emerald-600 rounded-lg text-white"
          >
            {mobileMenuOpen ? <X className="w-5 h-5" /> : <Menu className="w-5 h-5" />}
          </button>
        </div>
      </header>

      {/* MOBILE DRAWER MENU */}
      {mobileMenuOpen && (
        <div className="md:hidden bg-slate-900 text-white border-b border-slate-800 p-3 space-y-1">
          {navItems.map((item) => {
            const Icon = item.icon;
            return (
              <button
                key={item.id}
                onClick={() => {
                  setActiveTab(item.id);
                  setMobileMenuOpen(false);
                }}
                className={`w-full flex items-center justify-between px-4 py-2.5 rounded-xl text-sm font-medium ${
                  activeTab === item.id ? 'bg-emerald-600 text-white' : 'text-slate-300'
                }`}
              >
                <span className="flex items-center gap-3">
                  <Icon className="w-4 h-4" />
                  {item.label}
                </span>
                {item.badge > 0 && (
                  <span className="px-2 py-0.5 text-xs bg-rose-500 rounded-full">{toBn(item.badge)}</span>
                )}
              </button>
            );
          })}
          <button
            onClick={() => setCurrentUser(null)}
            className="w-full flex items-center gap-3 px-4 py-2.5 rounded-xl text-sm font-medium text-rose-400"
          >
            <LogOut className="w-4 h-4" /> লগ আউট
          </button>
        </div>
      )}

      {/* MAIN CONTENT AREA */}
      <main className="flex-1 p-4 sm:p-6 lg:p-8 overflow-y-auto max-w-7xl mx-auto w-full">
        {/* Top Page Header */}
        <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6 bg-white p-4 sm:p-5 rounded-2xl shadow-sm border border-slate-200/80">
          <div>
            <div className="flex items-center gap-2">
              <h1 className="text-xl sm:text-2xl font-extrabold text-slate-900">{settings.societyName}</h1>
              {isAdmin && (
                <button
                  onClick={() => setActiveTab('settings')}
                  className="inline-flex items-center gap-1 px-2.5 py-1 bg-emerald-50 hover:bg-emerald-100 text-emerald-700 text-xs font-semibold rounded-lg border border-emerald-200 transition"
                >
                  <Edit3 className="w-3.5 h-3.5" /> নাম ও লোগো এডিট
                </button>
              )}
            </div>
            <p className="text-xs sm:text-sm text-slate-500 mt-0.5">
              স্বাগতম, <span className="font-semibold text-slate-700">{currentUser.name}</span> ({ROLE_LABELS[currentUser.role]})
            </p>
          </div>
          <div className="flex flex-wrap gap-2">
            <button
              onClick={() => setActiveTab('payments')}
              className="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white text-xs sm:text-sm font-semibold rounded-xl shadow-sm flex items-center gap-1.5 transition"
            >
              <CreditCard className="w-4 h-4" /> চাঁদা / কিস্তি জমা দিন
            </button>
            <button
              onClick={() => setLoanModalOpen(true)}
              className="px-4 py-2 bg-slate-800 hover:bg-slate-900 text-white text-xs sm:text-sm font-semibold rounded-xl shadow-sm flex items-center gap-1.5 transition"
            >
              <HandCoins className="w-4 h-4" /> লোনের আবেদন
            </button>
          </div>
        </div>

        {/* ====================================================================
            TAB 1: DASHBOARD & VISION/MISSION
           ==================================================================== */}
        {activeTab === 'dashboard' && (
          <div className="space-y-6">
            {/* Financial Summary Cards (All start from ৳০) */}
            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
              <div className="bg-gradient-to-br from-emerald-600 to-teal-700 text-white p-5 rounded-2xl shadow-lg">
                <div className="flex items-center justify-between">
                  <span className="text-emerald-100 text-sm font-medium">বর্তমান মোট তহবিল (ব্যালেন্স)</span>
                  <Wallet className="w-6 h-6 text-emerald-200" />
                </div>
                <p className="text-3xl font-extrabold mt-2">{formatCurrency(currentBalance)}</p>
                <p className="text-xs text-emerald-100 mt-2">শুরুতে ব্যালেন্স: ৳ ০ (শূন্য থেকে শুরু)</p>
              </div>

              <div className="bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
                <div className="flex items-center justify-between">
                  <span className="text-slate-500 text-sm font-medium">মোট মাসিক চাঁদা আদায়</span>
                  <TrendingUp className="w-6 h-6 text-emerald-600" />
                </div>
                <p className="text-2xl font-extrabold text-slate-800 mt-2">{formatCurrency(totalSubscription)}</p>
                <p className="text-xs text-slate-400 mt-2">সকল সদস্যের জমাকৃত চাঁদা</p>
              </div>

              <div className="bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
                <div className="flex items-center justify-between">
                  <span className="text-slate-500 text-sm font-medium">মোট লোনের কিস্তি আদায়</span>
                  <RefreshCw className="w-6 h-6 text-blue-600" />
                </div>
                <p className="text-2xl font-extrabold text-slate-800 mt-2">{formatCurrency(totalInstallment)}</p>
                <p className="text-xs text-slate-400 mt-2">পরিশোধিত কিস্তির মোট পরিমাণ</p>
              </div>

              <div className="bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
                <div className="flex items-center justify-between">
                  <span className="text-slate-500 text-sm font-medium">মোট আয় (চাঁদা + কিস্তি + অন্যান্য)</span>
                  <TrendingUp className="w-6 h-6 text-teal-600" />
                </div>
                <p className="text-2xl font-extrabold text-teal-700 mt-2">{formatCurrency(totalIncomeAll)}</p>
                <p className="text-xs text-slate-400 mt-2">অন্যান্য আয়: {formatCurrency(totalOtherIncome)}</p>
              </div>

              <div className="bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
                <div className="flex items-center justify-between">
                  <span className="text-slate-500 text-sm font-medium">মোট ব্যয় ও লোন বিতরণ</span>
                  <TrendingDown className="w-6 h-6 text-rose-600" />
                </div>
                <p className="text-2xl font-extrabold text-rose-600 mt-2">
                  {formatCurrency(totalExpense + totalApprovedLoanDisbursed)}
                </p>
                <p className="text-xs text-slate-400 mt-2">
                  ব্যয়: {formatCurrency(totalExpense)} | লোন বিতরণ: {formatCurrency(totalApprovedLoanDisbursed)}
                </p>
              </div>

              <div className="bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
                <div className="flex items-center justify-between">
                  <span className="text-slate-500 text-sm font-medium">নিবন্ধিত মোট সদস্য</span>
                  <Users className="w-6 h-6 text-indigo-600" />
                </div>
                <p className="text-2xl font-extrabold text-slate-800 mt-2">{toBn(members.length)} জন</p>
                <p className="text-xs text-slate-400 mt-2">
                  অপেক্ষমান লোন আবেদন: {toBn(loans.filter((l) => l.status === 'pending').length)} টি
                </p>
              </div>
            </div>

            {/* Society Vision & Mission Card (Editable by Admin) */}
            <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
              <div className="flex items-center justify-between mb-3">
                <div className="flex items-center gap-2.5">
                  <div className="p-2 bg-emerald-100 text-emerald-700 rounded-xl">
                    <Target className="w-5 h-5" />
                  </div>
                  <h2 className="text-lg font-bold text-slate-800">সমিতির লক্ষ্য ও উদ্দেশ্য</h2>
                </div>
                {isAdmin && (
                  <button
                    onClick={() => setActiveTab('settings')}
                    className="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold rounded-lg flex items-center gap-1.5 transition"
                  >
                    <Edit3 className="w-3.5 h-3.5" /> লক্ষ্য ও উদ্দেশ্য এডিট করুন
                  </button>
                )}
              </div>
              <p className="text-slate-600 text-sm sm:text-base leading-relaxed whitespace-pre-line bg-slate-50 p-4 rounded-xl border border-slate-100">
                {settings.visionMission}
              </p>
            </div>

            {/* Recent Transactions Preview */}
            <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
              <div className="flex items-center justify-between mb-4">
                <h3 className="text-lg font-bold text-slate-800">সাম্প্রতিক লেনদেনসমূহ</h3>
                <button
                  onClick={() => setActiveTab('ledger')}
                  className="text-xs font-semibold text-emerald-700 hover:underline"
                >
                  সব হিসাব দেখুন →
                </button>
              </div>
              {transactions.length === 0 ? (
                <div className="text-center py-8 text-slate-400 text-sm">
                  এখনও কোনো লেনদেন হয়নি। সব হিসাব ৳০ (শূন্য) থেকে শুরু হয়েছে।
                </div>
              ) : (
                <div className="overflow-x-auto">
                  <table className="w-full text-sm text-left">
                    <thead className="bg-slate-50 text-slate-600 font-semibold border-b">
                      <tr>
                        <th className="py-3 px-3">তারিখ</th>
                        <th className="py-3 px-3">বিবরণ / সদস্য</th>
                        <th className="py-3 px-3">ধরন</th>
                        <th className="py-3 px-3">মাধ্যম</th>
                        <th className="py-3 px-3 text-right">পরিমাণ</th>
                      </tr>
                    </thead>
                    <tbody className="divide-y divide-slate-100">
                      {transactions.slice(0, 6).map((tx) => (
                        <tr key={tx.id} className="hover:bg-slate-50">
                          <td className="py-3 px-3 text-slate-500">{tx.date}</td>
                          <td className="py-3 px-3 font-medium text-slate-800">
                            {tx.memberName}
                            {tx.month && <span className="text-xs text-slate-400 block">{tx.month} {tx.year}</span>}
                          </td>
                          <td className="py-3 px-3">
                            <span className={`px-2.5 py-0.5 rounded-full text-xs font-semibold ${
                              tx.type === 'expense'
                                ? 'bg-rose-100 text-rose-700'
                                : 'bg-emerald-100 text-emerald-700'
                            }`}>
                              {tx.type === 'subscription' ? 'মাসিক চাঁদা' :
                               tx.type === 'installment' ? 'লোনের কিস্তি' :
                               tx.type === 'income' ? 'অন্যান্য আয়' : 'ব্যয়'}
                            </span>
                          </td>
                          <td className="py-3 px-3 text-xs text-slate-500">{tx.methodName || 'ক্যাশ'}</td>
                          <td className={`py-3 px-3 text-right font-bold ${
                            tx.type === 'expense' ? 'text-rose-600' : 'text-emerald-700'
                          }`}>
                            {tx.type === 'expense' ? '-' : '+'} {formatCurrency(tx.amount)}
                          </td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              )}
            </div>
          </div>
        )}

        {/* ====================================================================
            TAB 2: MEMBERS & ADMIN MANAGEMENT
           ==================================================================== */}
        {activeTab === 'members' && (
          <div className="space-y-6">
            <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4 bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
              <div>
                <h2 className="text-lg font-bold text-slate-800">সমিতির সকল সদস্য ও পরিচালনা পর্ষদ</h2>
                <p className="text-xs text-slate-500">
                  এডমিন নতুন সদস্য যুক্ত করলে তারা মোবাইল নাম্বার ও পাসওয়ার্ড দিয়ে লগইন করতে পারবেন।
                </p>
              </div>
              {isAdmin && (
                <button
                  onClick={openAddMemberModal}
                  className="px-4 py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-bold rounded-xl shadow flex items-center gap-2 transition"
                >
                  <UserPlus className="w-4 h-4" /> নতুন সদস্য / এডমিন যুক্ত করুন
                </button>
              )}
            </div>

            {/* Members Grid */}
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
              {members.map((m) => (
                <div key={m.id} className="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden flex flex-col justify-between">
                  <div className="p-5">
                    <div className="flex items-start gap-4">
                      <div className="w-16 h-16 rounded-2xl bg-slate-100 border border-slate-200 flex items-center justify-center overflow-hidden shrink-0">
                        {m.photoUrl ? (
                          <img src={m.photoUrl} alt={m.name} className="w-full h-full object-cover" />
                        ) : (
                          <Users className="w-8 h-8 text-slate-400" />
                        )}
                      </div>
                      <div className="min-w-0 flex-1">
                        <div className="flex items-center justify-between gap-1">
                          <span className="text-[11px] font-bold px-2 py-0.5 bg-slate-100 text-slate-600 rounded">
                            {m.memberCode || 'ID'}
                          </span>
                          <span className={`text-[11px] font-bold px-2 py-0.5 rounded-full ${
                            m.role === 'main_admin' ? 'bg-purple-100 text-purple-700' :
                            m.role === 'admin' ? 'bg-blue-100 text-blue-700' :
                            m.role === 'cashier' ? 'bg-amber-100 text-amber-800' :
                            'bg-emerald-100 text-emerald-700'
                          }`}>
                            {ROLE_LABELS[m.role]}
                          </span>
                        </div>
                        <h3 className="font-bold text-slate-900 text-base mt-1 truncate">{m.name}</h3>
                        <p className="text-xs text-slate-500 mt-0.5">মোবাইল: {m.mobile}</p>
                        {m.nid && <p className="text-xs text-slate-500">NID: {m.nid}</p>}
                      </div>
                    </div>

                    <div className="mt-4 pt-3 border-t border-slate-100 text-xs text-slate-600 space-y-1">
                      <p><span className="text-slate-400">পিতার নাম:</span> {m.fatherName || '—'}</p>
                      <p><span className="text-slate-400">মাতার নাম:</span> {m.motherName || '—'}</p>
                      <p><span className="text-slate-400">স্বামী/স্ত্রী:</span> {m.spouseName || '—'}</p>
                      <p><span className="text-slate-400">নমিনি:</span> {m.nomineeName || '—'}</p>
                    </div>

                    {m.signatureUrl && (
                      <div className="mt-3 pt-2 border-t border-slate-100 flex items-center justify-between">
                        <span className="text-[11px] text-slate-400">সদস্যের স্বাক্ষর:</span>
                        <img src={m.signatureUrl} alt="Sign" className="h-8 object-contain border rounded px-1.5 bg-slate-50" />
                      </div>
                    )}
                  </div>

                  {/* Card Footer Actions */}
                  <div className="px-5 py-3 bg-slate-50 border-t border-slate-100 flex items-center justify-between gap-2">
                    <button
                      onClick={() => setViewMemberDetails(m)}
                      className="text-xs font-semibold text-slate-700 hover:text-emerald-700 flex items-center gap-1"
                    >
                      <Eye className="w-3.5 h-3.5" /> বিস্তারিত কার্ড
                    </button>

                    <div className="flex items-center gap-2">
                      {(isAdmin || currentUser.id === m.id) && (
                        <button
                          onClick={() => openEditMemberModal(m)}
                          className="px-2.5 py-1 bg-blue-50 hover:bg-blue-100 text-blue-700 rounded-lg text-xs font-semibold flex items-center gap-1 transition"
                        >
                          <Edit3 className="w-3.5 h-3.5" /> এডিট
                        </button>
                      )}
                      {isMainAdmin && m.role !== 'main_admin' && (
                        <button
                          onClick={() => handleDeleteMember(m)}
                          className="p-1.5 bg-rose-50 hover:bg-rose-100 text-rose-600 rounded-lg transition"
                          title="সদস্য মুছুন"
                        >
                          <Trash2 className="w-3.5 h-3.5" />
                        </button>
                      )}
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* ====================================================================
            TAB 3: SUBSCRIPTION & INSTALLMENT COLLECTION + ONLINE PAYMENT
           ==================================================================== */}
        {activeTab === 'payments' && (
          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            {/* Payment Form */}
            <div className="lg:col-span-2 bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
              <div className="flex items-center gap-2.5 mb-5">
                <div className="p-2.5 bg-emerald-100 text-emerald-700 rounded-xl">
                  <CreditCard className="w-6 h-6" />
                </div>
                <div>
                  <h2 className="text-lg font-bold text-slate-800">চাঁদা আদায় ও কিস্তি পরিশোধ (Online Payment)</h2>
                  <p className="text-xs text-slate-500">মাসের নাম, সাল, চাঁদা/কিস্তি, টাকার পরিমাণ ও অনলাইন পেমেন্ট মাধ্যম সিলেক্ট করুন</p>
                </div>
              </div>

              <form onSubmit={handlePaymentSubmit} className="space-y-4">
                {/* Member Selector */}
                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-1">সদস্য নির্বাচন করুন *</label>
                  {isAdmin || isCashier ? (
                    <select
                      required
                      value={paymentForm.memberId}
                      onChange={(e) => setPaymentForm({ ...paymentForm, memberId: e.target.value })}
                      className="w-full px-4 py-2.5 border border-slate-300 rounded-xl bg-white focus:ring-2 focus:ring-emerald-500 outline-none"
                    >
                      <option value="">-- সদস্য সিলেক্ট করুন --</option>
                      {members.map((m) => (
                        <option key={m.id} value={m.id}>
                          {m.name} ({m.mobile}) - {m.memberCode}
                        </option>
                      ))}
                    </select>
                  ) : (
                    <input
                      type="text"
                      disabled
                      value={`${currentUser.name} (${currentUser.mobile})`}
                      className="w-full px-4 py-2.5 border border-slate-200 rounded-xl bg-slate-100 text-slate-700 font-medium"
                    />
                  )}
                </div>

                {/* Payment Type (Subscription vs Installment) */}
                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-1">পেমেন্টের ধরন সিলেক্ট করুন *</label>
                  <div className="grid grid-cols-2 gap-3">
                    <button
                      type="button"
                      onClick={() => setPaymentForm({ ...paymentForm, type: 'subscription' })}
                      className={`py-3 px-4 rounded-xl border-2 text-sm font-bold transition ${
                        paymentForm.type === 'subscription'
                          ? 'border-emerald-600 bg-emerald-50 text-emerald-800'
                          : 'border-slate-200 bg-white text-slate-600'
                      }`}
                    >
                      মাসিক চাঁদা (Subscription)
                    </button>
                    <button
                      type="button"
                      onClick={() => setPaymentForm({ ...paymentForm, type: 'installment' })}
                      className={`py-3 px-4 rounded-xl border-2 text-sm font-bold transition ${
                        paymentForm.type === 'installment'
                          ? 'border-blue-600 bg-blue-50 text-blue-800'
                          : 'border-slate-200 bg-white text-slate-600'
                      }`}
                    >
                      লোনের কিস্তি (Installment)
                    </button>
                  </div>
                </div>

                {/* Month, Year & Amount */}
                <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
                  <div>
                    <label className="block text-sm font-semibold text-slate-700 mb-1">মাসের নাম *</label>
                    <select
                      value={paymentForm.month}
                      onChange={(e) => setPaymentForm({ ...paymentForm, month: e.target.value })}
                      className="w-full px-3.5 py-2.5 border border-slate-300 rounded-xl bg-white focus:ring-2 focus:ring-emerald-500 outline-none"
                    >
                      {MONTHS_BN.map((m) => (
                        <option key={m} value={m}>{m}</option>
                      ))}
                    </select>
                  </div>

                  <div>
                    <label className="block text-sm font-semibold text-slate-700 mb-1">সাল (Year) *</label>
                    <select
                      value={paymentForm.year}
                      onChange={(e) => setPaymentForm({ ...paymentForm, year: e.target.value })}
                      className="w-full px-3.5 py-2.5 border border-slate-300 rounded-xl bg-white focus:ring-2 focus:ring-emerald-500 outline-none"
                    >
                      {YEARS_BN.map((y) => (
                        <option key={y} value={y}>{y}</option>
                      ))}
                    </select>
                  </div>

                  <div>
                    <label className="block text-sm font-semibold text-slate-700 mb-1">টাকার পরিমাণ (৳) *</label>
                    <input
                      type="number"
                      required
                      min="1"
                      placeholder="যেমন: 500"
                      value={paymentForm.amount}
                      onChange={(e) => setPaymentForm({ ...paymentForm, amount: e.target.value })}
                      className="w-full px-3.5 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none font-bold"
                    />
                  </div>
                </div>

                {/* Online Payment Option Selector */}
                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-2">পেমেন্ট মাধ্যম (Online Payment Option) *</label>
                  <div className="grid grid-cols-2 sm:grid-cols-3 gap-2.5">
                    {PAYMENT_METHODS.map((pm) => (
                      <button
                        key={pm.id}
                        type="button"
                        onClick={() => setPaymentForm({ ...paymentForm, method: pm.id })}
                        className={`p-3 rounded-xl border-2 text-left transition flex items-center gap-2 ${
                          paymentForm.method === pm.id
                            ? 'border-emerald-600 bg-emerald-50/70 shadow-sm'
                            : 'border-slate-200 hover:border-slate-300'
                        }`}
                      >
                        <span className={`w-3 h-3 rounded-full shrink-0 ${pm.color}`}></span>
                        <span className="text-xs font-bold text-slate-800">{pm.name}</span>
                      </button>
                    ))}
                  </div>
                </div>

                {/* Online Payment Transaction ID */}
                {paymentForm.method !== 'cash' && (
                  <div className="p-4 bg-amber-50 border border-amber-200 rounded-xl space-y-2">
                    <p className="text-xs font-semibold text-amber-900">
                      অনলাইন পেমেন্ট ({PAYMENT_METHODS.find((m) => m.id === paymentForm.method)?.name}) সম্পন্ন করে নিচে Transaction ID দিন:
                    </p>
                    <input
                      type="text"
                      required
                      placeholder="Transaction ID / TrxID লিখুন (যেমন: 9H7K2L8P)"
                      value={paymentForm.trxId}
                      onChange={(e) => setPaymentForm({ ...paymentForm, trxId: e.target.value })}
                      className="w-full px-3.5 py-2 border border-amber-300 rounded-lg bg-white text-sm font-mono uppercase focus:ring-2 focus:ring-amber-500 outline-none"
                    />
                  </div>
                )}

                <div>
                  <label className="block text-sm font-semibold text-slate-700 mb-1">মন্তব্য (ঐচ্ছিক)</label>
                  <input
                    type="text"
                    placeholder="অতিরিক্ত কোনো নোট থাকলে লিখুন..."
                    value={paymentForm.note}
                    onChange={(e) => setPaymentForm({ ...paymentForm, note: e.target.value })}
                    className="w-full px-4 py-2 border border-slate-300 rounded-xl text-sm outline-none"
                  />
                </div>

                <button
                  type="submit"
                  className="w-full py-3.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg shadow-emerald-600/25 transition flex items-center justify-center gap-2"
                >
                  <CheckCircle className="w-5 h-5" /> পেমেন্ট নিশ্চিত করুন ও রশিদ নিন
                </button>
              </form>
            </div>

            {/* Recent Receipts List */}
            <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-5">
              <h3 className="font-bold text-slate-800 mb-3">সাম্প্রতিক চাঁদা ও কিস্তির রশিদ</h3>
              <div className="space-y-3 max-h-[540px] overflow-y-auto pr-1">
                {transactions.filter((t) => t.type === 'subscription' || t.type === 'installment').length === 0 ? (
                  <p className="text-xs text-slate-400 text-center py-8">এখনও কোনো চাঁদা বা কিস্তি জমা হয়নি।</p>
                ) : (
                  transactions
                    .filter((t) => t.type === 'subscription' || t.type === 'installment')
                    .map((tx) => (
                      <div key={tx.id} className="p-3.5 rounded-xl border border-slate-200 bg-slate-50 hover:bg-white transition">
                        <div className="flex items-center justify-between">
                          <span className="text-xs font-bold text-emerald-700">{tx.receiptNo}</span>
                          <span className="text-xs text-slate-400">{tx.date}</span>
                        </div>
                        <p className="font-bold text-slate-800 text-sm mt-1">{tx.memberName}</p>
                        <p className="text-xs text-slate-500">
                          {tx.type === 'subscription' ? 'মাসিক চাঁদা' : 'লোনের কিস্তি'} • {tx.month} {tx.year}
                        </p>
                        <div className="flex items-center justify-between mt-2 pt-2 border-t border-slate-200/70">
                          <span className="text-sm font-extrabold text-slate-900">{formatCurrency(tx.amount)}</span>
                          <button
                            onClick={() => setReceiptModalData(tx)}
                            className="text-xs font-semibold text-blue-600 hover:underline flex items-center gap-1"
                          >
                            <Printer className="w-3.5 h-3.5" /> রশিদ দেখুন
                          </button>
                        </div>
                      </div>
                    ))
                )}
              </div>
            </div>
          </div>
        )}

        {/* ====================================================================
            TAB 4: INCOME & EXPENSE LEDGER (আয়-ব্যয়ের হিসাব)
           ==================================================================== */}
        {activeTab === 'ledger' && (
          <div className="space-y-6">
            {(isAdmin || isCashier) && (
              <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                <h2 className="text-lg font-bold text-slate-800 mb-4">নতুন আয় বা ব্যয়ের হিসাব যুক্ত করুন</h2>
                <form onSubmit={handleLedgerSubmit} className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-3">
                  <div>
                    <label className="block text-xs font-bold text-slate-600 mb-1">হিসাবের ধরন</label>
                    <select
                      value={ledgerForm.type}
                      onChange={(e) => setLedgerForm({ ...ledgerForm, type: e.target.value })}
                      className="w-full px-3 py-2.5 border border-slate-300 rounded-xl bg-white text-sm font-semibold"
                    >
                      <option value="income">অন্যান্য আয় (+)</option>
                      <option value="expense">সমিতির ব্যয় (-)</option>
                    </select>
                  </div>
                  <div className="lg:col-span-2">
                    <label className="block text-xs font-bold text-slate-600 mb-1">খাতের নাম / বিবরণ *</label>
                    <input
                      type="text"
                      required
                      placeholder="যেমন: ভর্তি ফি, ব্যাংক মুনাফা বা অফিস খরচ"
                      value={ledgerForm.title}
                      onChange={(e) => setLedgerForm({ ...ledgerForm, title: e.target.value })}
                      className="w-full px-3 py-2.5 border border-slate-300 rounded-xl text-sm"
                    />
                  </div>
                  <div>
                    <label className="block text-xs font-bold text-slate-600 mb-1">টাকার পরিমাণ (৳) *</label>
                    <input
                      type="number"
                      required
                      min="1"
                      placeholder="0"
                      value={ledgerForm.amount}
                      onChange={(e) => setLedgerForm({ ...ledgerForm, amount: e.target.value })}
                      className="w-full px-3 py-2.5 border border-slate-300 rounded-xl text-sm font-bold"
                    />
                  </div>
                  <div className="flex items-end">
                    <button
                      type="submit"
                      className="w-full py-2.5 px-4 bg-slate-900 hover:bg-slate-800 text-white text-sm font-bold rounded-xl transition"
                    >
                      হিসাব যোগ করুন
                    </button>
                  </div>
                </form>
              </div>
            )}

            {/* Full Accounting Ledger Table */}
            <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
              <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-4">
                <h3 className="text-lg font-bold text-slate-800">সম্পূর্ণ আয়-ব্যয়ের লেজার খাতা</h3>
                <div className="text-sm font-bold text-emerald-700 bg-emerald-50 px-3 py-1.5 rounded-xl border border-emerald-200">
                  বর্তমান নিট তহবিল: {formatCurrency(currentBalance)}
                </div>
              </div>

              {transactions.length === 0 ? (
                <p className="text-center py-10 text-slate-400 text-sm">কোনো আয় বা ব্যয়ের রেকর্ড নেই (ব্যালেন্স: ৳ ০)।</p>
              ) : (
                <div className="overflow-x-auto">
                  <table className="w-full text-sm text-left">
                    <thead className="bg-slate-50 text-slate-600 font-semibold border-b">
                      <tr>
                        <th className="py-3 px-3">রশিদ/TRX</th>
                        <th className="py-3 px-3">তারিখ</th>
                        <th className="py-3 px-3">বিবরণ / সদস্য</th>
                        <th className="py-3 px-3">ধরন</th>
                        <th className="py-3 px-3">মাধ্যম</th>
                        <th className="py-3 px-3 text-right">টাকার পরিমাণ</th>
                      </tr>
                    </thead>
                    <tbody className="divide-y divide-slate-100">
                      {transactions.map((tx) => (
                        <tr key={tx.id} className="hover:bg-slate-50">
                          <td className="py-3 px-3 font-mono text-xs text-slate-500">{tx.receiptNo}</td>
                          <td className="py-3 px-3 text-slate-500">{tx.date}</td>
                          <td className="py-3 px-3 font-medium text-slate-800">
                            {tx.memberName || tx.title}
                            {tx.month && <span className="text-xs text-slate-400 ml-1">({tx.month} {tx.year})</span>}
                          </td>
                          <td className="py-3 px-3">
                            <span className={`px-2.5 py-0.5 rounded-full text-xs font-semibold ${
                              tx.type === 'expense' ? 'bg-rose-100 text-rose-700' : 'bg-emerald-100 text-emerald-700'
                            }`}>
                              {tx.type === 'subscription' ? 'মাসিক চাঁদা' :
                               tx.type === 'installment' ? 'লোনের কিস্তি' :
                               tx.type === 'income' ? 'অন্যান্য আয়' : 'ব্যয়'}
                            </span>
                          </td>
                          <td className="py-3 px-3 text-xs text-slate-500">{tx.methodName || 'ক্যাশ'}</td>
                          <td className={`py-3 px-3 text-right font-bold ${
                            tx.type === 'expense' ? 'text-rose-600' : 'text-emerald-700'
                          }`}>
                            {tx.type === 'expense' ? '-' : '+'} {formatCurrency(tx.amount)}
                          </td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              )}
            </div>
          </div>
        )}

        {/* ====================================================================
            TAB 5: LOAN APPLICATIONS & ADMIN APPROVAL
           ==================================================================== */}
        {activeTab === 'loans' && (
          <div className="space-y-6">
            <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4 bg-white p-5 rounded-2xl shadow-sm border border-slate-200">
              <div>
                <h2 className="text-lg font-bold text-slate-800">লোন আবেদন ও অনুমোদন ব্যবস্থাপনা</h2>
                <p className="text-xs text-slate-500">
                  সদস্য লোনের আবেদন করলে এডমিন অনুমোদন দেওয়ার সাথে সাথে ক্যাশিয়ারের নিকট অটোমেটিক মেসেজ চলে যাবে।
                </p>
              </div>
              <button
                onClick={() => setLoanModalOpen(true)}
                className="px-4 py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-bold rounded-xl shadow flex items-center gap-2 transition"
              >
                <Plus className="w-4 h-4" /> নতুন লোনের আবেদন করুন
              </button>
            </div>

            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              {loans.length === 0 ? (
                <div className="col-span-full bg-white rounded-2xl p-10 text-center text-slate-400 text-sm border border-slate-200">
                  এখনও কোনো লোনের আবেদন জমা পড়েনি।
                </div>
              ) : (
                loans.map((loan) => (
                  <div key={loan.id} className="bg-white rounded-2xl shadow-sm border border-slate-200 p-5 flex flex-col justify-between">
                    <div>
                      <div className="flex items-center justify-between mb-2">
                        <span className="text-xs text-slate-400">আবেদনের তারিখ: {loan.appliedDate}</span>
                        <span className={`px-2.5 py-0.5 rounded-full text-xs font-bold ${
                          loan.status === 'approved' ? 'bg-emerald-100 text-emerald-700' :
                          loan.status === 'rejected' ? 'bg-rose-100 text-rose-700' :
                          'bg-amber-100 text-amber-800'
                        }`}>
                          {loan.status === 'approved' ? 'অনুমোদিত (Approved)' :
                           loan.status === 'rejected' ? 'বাতিল (Rejected)' : 'অপেক্ষমান (Pending)'}
                        </span>
                      </div>

                      <h3 className="text-base font-bold text-slate-900">{loan.memberName}</h3>
                      <p className="text-xs text-slate-500">মোবাইল: {loan.memberMobile} • আইডি: {loan.memberCode}</p>

                      <div className="mt-3 p-3 bg-slate-50 rounded-xl border border-slate-100 flex items-center justify-between">
                        <div>
                          <p className="text-xs text-slate-500">আবেদনকৃত লোনের পরিমাণ</p>
                          <p className="text-xl font-extrabold text-emerald-700">{formatCurrency(loan.amount)}</p>
                        </div>
                        <div className="text-right">
                          <p className="text-xs text-slate-500">কিস্তি সংখ্যা</p>
                          <p className="text-sm font-bold text-slate-800">{toBn(loan.installments)} টি কিস্তি</p>
                        </div>
                      </div>

                      <p className="text-xs text-slate-600 mt-3">
                        <span className="font-semibold">লোনের কারণ:</span> {loan.purpose}
                      </p>
                    </div>

                    {isAdmin && loan.status === 'pending' && (
                      <div className="mt-4 pt-3 border-t border-slate-100 flex gap-2">
                        <button
                          onClick={() => handleLoanDecision(loan, 'approved')}
                          className="flex-1 py-2 bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition"
                        >
                          <Check className="w-4 h-4" /> অনুমোদন দিন (ক্যাশিয়ারকে জানান)
                        </button>
                        <button
                          onClick={() => handleLoanDecision(loan, 'rejected')}
                          className="px-4 py-2 bg-rose-100 hover:bg-rose-200 text-rose-700 text-xs font-bold rounded-xl transition"
                        >
                          বাতিল
                        </button>
                      </div>
                    )}

                    {loan.status === 'approved' && (
                      <div className="mt-3 pt-2 border-t border-slate-100 text-[11px] text-emerald-700 font-medium flex items-center gap-1">
                        <CheckCircle className="w-3.5 h-3.5" /> অনুমোদিত ও ক্যাশিয়ারের নিকট মেসেজ প্রেরিত
                      </div>
                    )}
                  </div>
                ))
              )}
            </div>
          </div>
        )}

        {/* ====================================================================
            TAB 6: CASHIER NOTIFICATION INBOX
           ==================================================================== */}
        {activeTab === 'notifications' && (
          <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
            <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-5">
              <div className="flex items-center gap-2.5">
                <div className="p-2.5 bg-amber-100 text-amber-700 rounded-xl">
                  <Bell className="w-6 h-6" />
                </div>
                <div>
                  <h2 className="text-lg font-bold text-slate-800">ক্যাশিয়ার নোটিফিকেশন ও লোন অনুমোদন মেসেজ</h2>
                  <p className="text-xs text-slate-500">এডমিন কোনো লোন অনুমোদন করলে স্বয়ংক্রিয়ভাবে এখানে ক্যাশিয়ারের জন্য বার্তা আসে</p>
                </div>
              </div>
              {unreadCashierNotifs > 0 && (
                <button
                  onClick={markAllNotificationsRead}
                  className="px-3.5 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-xl transition"
                >
                  সবগুলো পঠিত করুন
                </button>
              )}
            </div>

            {notifications.length === 0 ? (
              <div className="text-center py-12 text-slate-400 text-sm">
                ক্যাশিয়ারের জন্য এখনও কোনো লোন অনুমোদনের মেসেজ আসেনি।
              </div>
            ) : (
              <div className="space-y-3">
                {notifications.map((n) => (
                  <div
                    key={n.id}
                    className={`p-4 rounded-2xl border transition ${
                      n.read ? 'bg-slate-50 border-slate-200' : 'bg-emerald-50/70 border-emerald-300 shadow-sm'
                    }`}
                  >
                    <div className="flex items-center justify-between mb-1.5">
                      <span className="inline-flex items-center gap-1.5 text-xs font-bold text-emerald-800">
                        <Send className="w-3.5 h-3.5" /> ক্যাশিয়ার বার্তা ({n.cashierName})
                      </span>
                      <span className="text-xs text-slate-400">
                        {new Date(n.createdAt).toLocaleString('bn-BD')}
                      </span>
                    </div>
                    <p className="text-sm text-slate-800 leading-relaxed font-medium">{n.message}</p>
                  </div>
                ))}
              </div>
            )}
          </div>
        )}

        {/* ====================================================================
            TAB 7: SOCIETY SETTINGS (EDIT NAME, LOGO, VISION & MISSION)
           ==================================================================== */}
        {activeTab === 'settings' && isAdmin && (
          <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 max-w-3xl">
            <div className="flex items-center gap-2.5 mb-5">
              <div className="p-2.5 bg-emerald-100 text-emerald-700 rounded-xl">
                <Settings className="w-6 h-6" />
              </div>
              <div>
                <h2 className="text-lg font-bold text-slate-800">সমিতির নাম, লোগো ও লক্ষ্য-উদ্দেশ্য পরিবর্তন</h2>
                <p className="text-xs text-slate-500">যেকোনো সময় অ্যাপের নাম, লোগো এবং সমিতির লক্ষ্য ও উদ্দেশ্য এডিট করতে পারবেন</p>
              </div>
            </div>

            <form onSubmit={handleSaveSettings} className="space-y-5">
              <div>
                <label className="block text-sm font-bold text-slate-700 mb-1">সমিতি / অ্যাপের নাম *</label>
                <input
                  type="text"
                  required
                  value={settingsForm.societyName}
                  onChange={(e) => setSettingsForm({ ...settingsForm, societyName: e.target.value })}
                  className="w-full px-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none font-bold"
                />
              </div>

              <div>
                <label className="block text-sm font-bold text-slate-700 mb-1">স্লোগান / ট্যাগলাইন</label>
                <input
                  type="text"
                  value={settingsForm.tagline}
                  onChange={(e) => setSettingsForm({ ...settingsForm, tagline: e.target.value })}
                  className="w-full px-4 py-2.5 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none"
                />
              </div>

              <div>
                <label className="block text-sm font-bold text-slate-700 mb-2">সমিতির লোগো সেট বা পরিবর্তন করুন</label>
                <div className="flex items-center gap-4">
                  <div className="w-20 h-20 rounded-2xl bg-slate-100 border-2 border-dashed border-slate-300 flex items-center justify-center overflow-hidden">
                    {settingsForm.logoUrl ? (
                      <img src={settingsForm.logoUrl} alt="Logo Preview" className="w-full h-full object-cover" />
                    ) : (
                      <Building2 className="w-8 h-8 text-slate-400" />
                    )}
                  </div>
                  <div className="space-y-2">
                    <label className="cursor-pointer inline-flex items-center gap-2 px-4 py-2 bg-slate-800 hover:bg-slate-900 text-white text-xs font-bold rounded-xl transition">
                      <Upload className="w-4 h-4" /> লোগো আপলোড করুন
                      <input type="file" accept="image/*" onChange={handleLogoUpload} className="hidden" />
                    </label>
                    {settingsForm.logoUrl && (
                      <button
                        type="button"
                        onClick={() => setSettingsForm({ ...settingsForm, logoUrl: '' })}
                        className="block text-xs text-rose-600 hover:underline"
                      >
                        লোগো মুছে ফেলুন
                      </button>
                    )}
                  </div>
                </div>
              </div>

              <div>
                <label className="block text-sm font-bold text-slate-700 mb-1">সমিতির লক্ষ্য ও উদ্দেশ্য *</label>
                <textarea
                  rows="5"
                  required
                  value={settingsForm.visionMission}
                  onChange={(e) => setSettingsForm({ ...settingsForm, visionMission: e.target.value })}
                  className="w-full px-4 py-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none text-sm leading-relaxed"
                />
              </div>

              <button
                type="submit"
                className="px-6 py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg transition"
              >
                পরিবর্তন সংরক্ষণ করুন
              </button>
            </form>
          </div>
        )}
      </main>

      {/* ======================================================================
          MODAL 1: ADD / EDIT MEMBER (FULL DETAILS + PHOTO + SIGNATURE + ROLE)
         ====================================================================== */}
      {memberModalOpen && (
        <div className="fixed inset-0 z-50 bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-4 overflow-y-auto">
          <div className="bg-white rounded-3xl shadow-2xl max-w-2xl w-full max-h-[92vh] overflow-y-auto border border-slate-200">
            <div className="sticky top-0 bg-white px-6 py-4 border-b border-slate-200 flex items-center justify-between z-10">
              <h3 className="text-lg font-bold text-slate-800">
                {editingMember ? `${editingMember.name}-এর তথ্য এডিট করুন` : 'নতুন সদস্য / এডমিন যুক্ত করুন'}
              </h3>
              <button
                onClick={() => setMemberModalOpen(false)}
                className="p-1.5 bg-slate-100 hover:bg-slate-200 rounded-full text-slate-600"
              >
                <X className="w-5 h-5" />
              </button>
            </div>

            <form onSubmit={handleSaveMember} className="p-6 space-y-4">
              {/* Role Selector (Main Admin can assign Admin or Cashier) */}
              <div className="p-3.5 bg-emerald-50 border border-emerald-200 rounded-2xl">
                <label className="block text-xs font-bold text-emerald-900 mb-1">পদবি / রোল নির্বাচন করুন *</label>
                <select
                  value={memberForm.role}
                  disabled={editingMember?.role === 'main_admin'}
                  onChange={(e) => setMemberForm({ ...memberForm, role: e.target.value })}
                  className="w-full px-3.5 py-2 border border-emerald-300 rounded-xl bg-white text-sm font-bold text-slate-800 outline-none"
                >
                  {editingMember?.role === 'main_admin' && (
                    <option value="main_admin">মেইন এডমিন (Main Admin)</option>
                  )}
                  <option value="member">সাধারণ সদস্য (Member)</option>
                  <option value="cashier">ক্যাশিয়ার (Cashier - লোন মেসেজ পাবেন)</option>
                  {isMainAdmin && <option value="admin">সহকারী এডমিন (Admin)</option>}
                </select>
              </div>

              {/* Photo Upload */}
              <div className="flex items-center gap-4">
                <div className="w-20 h-20 rounded-2xl bg-slate-100 border border-slate-300 flex items-center justify-center overflow-hidden shrink-0">
                  {memberForm.photoUrl ? (
                    <img src={memberForm.photoUrl} alt="Member" className="w-full h-full object-cover" />
                  ) : (
                    <Users className="w-8 h-8 text-slate-400" />
                  )}
                </div>
                <div>
                  <label className="cursor-pointer inline-flex items-center gap-2 px-4 py-2 bg-slate-800 hover:bg-slate-900 text-white text-xs font-bold rounded-xl transition">
                    <Upload className="w-4 h-4" /> সদস্যের ছবি আপলোড দিন
                    <input type="file" accept="image/*" onChange={handlePhotoUpload} className="hidden" />
                  </label>
                  <p className="text-[11px] text-slate-400 mt-1">পাসপোর্ট সাইজ বা স্পষ্ট ছবি নির্বাচন করুন</p>
                </div>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">সদস্যের নাম *</label>
                  <input
                    type="text"
                    required
                    placeholder="পূর্ণ নাম"
                    value={memberForm.name}
                    onChange={(e) => setMemberForm({ ...memberForm, name: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">মোবাইল নাম্বার (লগইন ও OTP-র জন্য) *</label>
                  <input
                    type="text"
                    required
                    placeholder="01XXXXXXXXX"
                    value={memberForm.mobile}
                    onChange={(e) => setMemberForm({ ...memberForm, mobile: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">পিতার নাম *</label>
                  <input
                    type="text"
                    required
                    placeholder="পিতার নাম লিখুন"
                    value={memberForm.fatherName}
                    onChange={(e) => setMemberForm({ ...memberForm, fatherName: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">মাতার নাম *</label>
                  <input
                    type="text"
                    required
                    placeholder="মাতার নাম লিখুন"
                    value={memberForm.motherName}
                    onChange={(e) => setMemberForm({ ...memberForm, motherName: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">স্বামীর নাম / স্ত্রীর নাম</label>
                  <input
                    type="text"
                    placeholder="স্বামী বা স্ত্রীর নাম"
                    value={memberForm.spouseName}
                    onChange={(e) => setMemberForm({ ...memberForm, spouseName: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">নমিনির নাম *</label>
                  <input
                    type="text"
                    required
                    placeholder="নমিনির নাম লিখুন"
                    value={memberForm.nomineeName}
                    onChange={(e) => setMemberForm({ ...memberForm, nomineeName: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">জাতীয় পরিচয়পত্র নম্বর (NID) *</label>
                  <input
                    type="text"
                    required
                    placeholder="NID নম্বর লিখুন"
                    value={memberForm.nid}
                    onChange={(e) => setMemberForm({ ...memberForm, nid: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                  />
                </div>
                <div>
                  <label className="block text-xs font-bold text-slate-700 mb-1">লগইন পাসওয়ার্ড সেট করুন *</label>
                  <input
                    type="text"
                    required
                    placeholder="সদস্যের লগইন পাসওয়ার্ড"
                    value={memberForm.password}
                    onChange={(e) => setMemberForm({ ...memberForm, password: e.target.value })}
                    className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm font-mono"
                  />
                </div>
              </div>

              {/* Digital Signature Pad / Upload */}
              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">সদস্যের স্বাক্ষর / সাইন (Signature)</label>
                <SignaturePad
                  value={memberForm.signatureUrl}
                  onChange={(val) => setMemberForm((prev) => ({ ...prev, signatureUrl: val }))}
                />
              </div>

              <div className="flex justify-end gap-3 pt-3 border-t border-slate-200">
                <button
                  type="button"
                  onClick={() => setMemberModalOpen(false)}
                  className="px-5 py-2.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-sm font-bold rounded-xl"
                >
                  বাতিল
                </button>
                <button
                  type="submit"
                  className="px-6 py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-bold rounded-xl shadow-lg"
                >
                  তথ্য সংরক্ষণ করুন
                </button>
              </div>
            </form>
          </div>
        </div>
      )}

      {/* ======================================================================
          MODAL 2: VIEW MEMBER ID CARD & FULL PROFILE
         ====================================================================== */}
      {viewMemberDetails && (
        <div className="fixed inset-0 z-50 bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-3xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-200">
            <div className="bg-gradient-to-r from-emerald-700 to-teal-700 p-5 text-white flex items-center justify-between">
              <div>
                <h3 className="font-bold text-base">{settings.societyName}</h3>
                <p className="text-xs text-emerald-100">সদস্য পরিচিতি পত্র (Member Profile)</p>
              </div>
              <button onClick={() => setViewMemberDetails(null)} className="p-1 bg-white/20 rounded-full">
                <X className="w-5 h-5" />
              </button>
            </div>
            <div className="p-6 space-y-4">
              <div className="flex items-center gap-4">
                <div className="w-20 h-20 rounded-2xl bg-slate-100 border border-slate-200 overflow-hidden flex items-center justify-center shrink-0">
                  {viewMemberDetails.photoUrl ? (
                    <img src={viewMemberDetails.photoUrl} alt={viewMemberDetails.name} className="w-full h-full object-cover" />
                  ) : (
                    <Users className="w-10 h-10 text-slate-400" />
                  )}
                </div>
                <div>
                  <span className="text-xs font-bold px-2.5 py-0.5 bg-emerald-100 text-emerald-800 rounded-full">
                    {ROLE_LABELS[viewMemberDetails.role]}
                  </span>
                  <h4 className="text-lg font-extrabold text-slate-900 mt-1">{viewMemberDetails.name}</h4>
                  <p className="text-xs text-slate-500">সদস্য আইডি: {viewMemberDetails.memberCode}</p>
                </div>
              </div>

              <div className="bg-slate-50 p-4 rounded-2xl border border-slate-200/80 text-xs space-y-2">
                <div className="flex justify-between"><span className="text-slate-500">পিতার নাম:</span><span className="font-bold">{viewMemberDetails.fatherName || '—'}</span></div>
                <div className="flex justify-between"><span className="text-slate-500">মাতার নাম:</span><span className="font-bold">{viewMemberDetails.motherName || '—'}</span></div>
                <div className="flex justify-between"><span className="text-slate-500">স্বামী/স্ত্রীর নাম:</span><span className="font-bold">{viewMemberDetails.spouseName || '—'}</span></div>
                <div className="flex justify-between"><span className="text-slate-500">নমিনির নাম:</span><span className="font-bold">{viewMemberDetails.nomineeName || '—'}</span></div>
                <div className="flex justify-between"><span className="text-slate-500">জাতীয় পরিচয়পত্র (NID):</span><span className="font-bold">{viewMemberDetails.nid || '—'}</span></div>
                <div className="flex justify-between"><span className="text-slate-500">মোবাইল নাম্বার:</span><span className="font-bold">{viewMemberDetails.mobile}</span></div>
              </div>

              {viewMemberDetails.signatureUrl && (
                <div className="flex items-center justify-between pt-2">
                  <span className="text-xs text-slate-500">স্বাক্ষর:</span>
                  <img src={viewMemberDetails.signatureUrl} alt="Sign" className="h-12 object-contain border rounded-lg px-3 py-1 bg-slate-50" />
                </div>
              )}

              <button
                onClick={() => window.print()}
                className="w-full py-2.5 bg-slate-900 text-white text-xs font-bold rounded-xl flex items-center justify-center gap-2"
              >
                <Printer className="w-4 h-4" /> প্রিন্ট / সেভ করুন
              </button>
            </div>
          </div>
        </div>
      )}

      {/* ======================================================================
          MODAL 3: DIGITAL PAYMENT RECEIPT
         ====================================================================== */}
      {receiptModalData && (
        <div className="fixed inset-0 z-50 bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-3xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-200">
            <div className="bg-emerald-700 p-5 text-white text-center relative">
              <button
                onClick={() => setReceiptModalData(null)}
                className="absolute right-4 top-4 p-1 bg-white/20 rounded-full"
              >
                <X className="w-4 h-4" />
              </button>
              <CheckCircle className="w-10 h-10 mx-auto text-emerald-200 mb-1" />
              <h3 className="font-bold text-lg">{settings.societyName}</h3>
              <p className="text-xs text-emerald-100">ডিজিটাল পেমেন্ট রশিদ (Money Receipt)</p>
            </div>

            <div className="p-6 space-y-3 text-sm">
              <div className="flex justify-between border-b pb-2">
                <span className="text-slate-500">রশিদ নং:</span>
                <span className="font-mono font-bold text-slate-800">{receiptModalData.receiptNo}</span>
              </div>
              <div className="flex justify-between border-b pb-2">
                <span className="text-slate-500">তারিখ:</span>
                <span className="font-semibold">{receiptModalData.date}</span>
              </div>
              <div className="flex justify-between border-b pb-2">
                <span className="text-slate-500">সদস্যের নাম:</span>
                <span className="font-bold text-slate-900">{receiptModalData.memberName}</span>
              </div>
              <div className="flex justify-between border-b pb-2">
                <span className="text-slate-500">বাবদ:</span>
                <span className="font-semibold">
                  {receiptModalData.type === 'subscription' ? 'মাসিক চাঁদা' : 'লোনের কিস্তি'} ({receiptModalData.month} {receiptModalData.year})
                </span>
              </div>
              <div className="flex justify-between border-b pb-2">
                <span className="text-slate-500">পেমেন্ট মাধ্যম:</span>
                <span className="font-semibold">{receiptModalData.methodName}</span>
              </div>
              {receiptModalData.trxId && receiptModalData.trxId !== 'CASH' && (
                <div className="flex justify-between border-b pb-2">
                  <span className="text-slate-500">Transaction ID:</span>
                  <span className="font-mono font-bold text-amber-700">{receiptModalData.trxId}</span>
                </div>
              )}
              <div className="p-3 bg-emerald-50 rounded-xl flex justify-between items-center mt-2">
                <span className="font-bold text-emerald-900">মোট পরিশোধিত টাকা:</span>
                <span className="text-xl font-extrabold text-emerald-700">{formatCurrency(receiptModalData.amount)}</span>
              </div>

              <button
                onClick={() => window.print()}
                className="w-full py-2.5 bg-slate-900 hover:bg-slate-800 text-white font-bold rounded-xl mt-3 flex items-center justify-center gap-2"
              >
                <Printer className="w-4 h-4" /> রশিদ প্রিন্ট করুন
              </button>
            </div>
          </div>
        </div>
      )}

      {/* ======================================================================
          MODAL 4: LOAN APPLICATION MODAL
         ====================================================================== */}
      {loanModalOpen && (
        <div className="fixed inset-0 z-50 bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-3xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-200">
            <div className="px-6 py-4 bg-slate-900 text-white flex items-center justify-between">
              <h3 className="font-bold text-base">নতুন লোনের আবেদন ফরম</h3>
              <button onClick={() => setLoanModalOpen(false)} className="p-1 bg-white/10 rounded-full">
                <X className="w-5 h-5" />
              </button>
            </div>

            <form onSubmit={handleLoanApply} className="p-6 space-y-4">
              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">আবেদনকারীর নাম</label>
                <input
                  type="text"
                  disabled
                  value={`${currentUser.name} (${currentUser.mobile})`}
                  className="w-full px-3.5 py-2 border border-slate-200 rounded-xl bg-slate-100 text-sm font-medium"
                />
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">লোনের টাকার পরিমাণ (৳) *</label>
                <input
                  type="number"
                  required
                  min="100"
                  placeholder="যেমন: 10000"
                  value={loanForm.amount}
                  onChange={(e) => setLoanForm({ ...loanForm, amount: e.target.value })}
                  className="w-full px-3.5 py-2.5 border border-slate-300 rounded-xl text-sm font-bold"
                />
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">কতটি কিস্তিতে পরিশোধ করবেন?</label>
                <select
                  value={loanForm.installments}
                  onChange={(e) => setLoanForm({ ...loanForm, installments: e.target.value })}
                  className="w-full px-3.5 py-2.5 border border-slate-300 rounded-xl bg-white text-sm"
                >
                  <option value="3">৩ টি মাসিক কিস্তি</option>
                  <option value="6">৬ টি মাসিক কিস্তি</option>
                  <option value="12">১২ টি মাসিক কিস্তি</option>
                  <option value="18">১৮ টি মাসিক কিস্তি</option>
                  <option value="24">২৪ টি মাসিক কিস্তি</option>
                </select>
              </div>

              <div>
                <label className="block text-xs font-bold text-slate-700 mb-1">লোন নেওয়ার কারণ / বিবরণ *</label>
                <textarea
                  rows="3"
                  required
                  placeholder="কি প্রয়োজনে লোন নিতে চাচ্ছেন তা লিখুন..."
                  value={loanForm.purpose}
                  onChange={(e) => setLoanForm({ ...loanForm, purpose: e.target.value })}
                  className="w-full px-3.5 py-2 border border-slate-300 rounded-xl text-sm"
                />
              </div>

              <button
                type="submit"
                className="w-full py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg transition"
              >
                আবেদন জমা দিন
              </button>
            </form>
          </div>
        </div>
      )}
    </div>
  );
}