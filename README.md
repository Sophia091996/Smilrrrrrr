import React, { useState, useEffect } from 'react';
import { 
  Wallet, 
  ArrowRightLeft, 
  PieChart, 
  Settings, 
  Bell, 
  Search, 
  Menu, 
  X,
  ArrowUpRight,
  ArrowDownLeft,
  CreditCard,
  User,
  LogOut,
  ChevronRight,
  Shield,
  Smartphone,
  Eye,
  EyeOff,
  Lock,
  HelpCircle,
  KeyRound,
  FileText,
  Building,
  AlertCircle,
  Zap,
  Calendar,
  DollarSign,
  Mail,
  MapPin,
  Phone,
  Edit2
} from 'lucide-react';

// --- Mock Data ---
const INITIAL_DATA = {
  user: {
    name: "Sophia Pierson",
    id: "88349210",
    lastLogin: "Today, 10:23 AM",
    email: "Sophiapiersonpage@gmail.com",
    phone: "+12153447209",
    address: "5678 Sophia St, Vancouver, BC V5W 2S7 Canada"
  },
  accounts: [
    { id: 1, type: "Checking", name: "Everyday Checking", balance: 998890.50, number: "**** 4521", color: "from-red-600 to-red-800" },
    { id: 2, type: "Savings", name: "Way2Save®", balance: 857945.20, number: "**** 9932", color: "from-emerald-600 to-emerald-800" },
    { 
      id: 3, 
      type: "Credit", 
      name: "Active Cash®", 
      balance: 0.00, 
      limit: 450000, 
      number: "**** 1122", 
      color: "from-slate-700 to-slate-900",
      rewards: 124.50,
      apr: "14.99%",
      dueDate: "Nov 28"
    }
  ],
  transactions: [
    { id: 101, title: "Netflix Subscription", date: "Today", amount: -15.99, type: "debit", category: "Entertainment", icon: "🎬" },
    { id: 102, title: "Salary Deposit", date: "Yesterday", amount: 3200.00, type: "credit", category: "Income", icon: "💰" },
    { id: 103, title: "Grocery Store", date: "Oct 24", amount: -142.50, type: "debit", category: "Food", icon: "🛒" },
    { id: 104, title: "Electric Bill", date: "Oct 22", amount: -85.00, type: "debit", category: "Utilities", icon: "⚡" },
    { id: 105, title: "Transfer from Savings", date: "Oct 20", amount: 500.00, type: "credit", category: "Transfer", icon: "💸" },
  ],
  payees: [
    { id: 1, name: "PG&E Electric", lastPaid: "Sep 15" },
    { id: 2, name: "Verizon Wireless", lastPaid: "Oct 01" },
    { id: 3, name: "State Farm Insurance", lastPaid: "Sep 28" },
    { id: 4, name: "Chase Credit Card", lastPaid: "Oct 10" }
  ]
};

// --- Components ---

const LoginScreen = ({ onLogin }) => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    setError('');
    setIsLoading(true);
    
    // Simulate API verification
    setTimeout(() => {
      if (username === 'Sophia2031' && password === 'LovelyGod') {
        onLogin(username);
      } else {
        setError('We do not recognize your username or password. Please try again.');
        setIsLoading(false);
      }
    }, 1500);
  };

  return (
    <div className="min-h-screen bg-slate-100 flex flex-col font-sans">
      {/* Official Header */}
      <header className="bg-red-600 h-20 flex items-center px-6 lg:px-12 shadow-md">
         <div className="w-10 h-10 bg-white rounded-md flex items-center justify-center text-red-600 font-bold text-xl shadow-sm">C</div>
         <span className="font-bold text-2xl tracking-tight text-white ml-3">Canada Bank</span>
      </header>

      {/* Main Login Area */}
      <main className="flex-1 flex items-center justify-center p-4 bg-gradient-to-b from-red-600 to-slate-100 h-64 bg-[length:100%_300px] bg-no-repeat">
        <div className="w-full max-w-4xl grid md:grid-cols-2 gap-8 items-start mt-[-60px]">
            
            {/* Login Box */}
            <div className="bg-white rounded-xl shadow-xl overflow-hidden border border-slate-200">
                <div className="p-8">
                <h1 className="text-2xl font-bold text-slate-800 mb-6">Sign On</h1>
                
                {error && (
                  <div className="mb-6 p-4 bg-red-50 border-l-4 border-red-600 text-red-800 text-sm rounded-r flex items-start gap-3">
                    <AlertCircle className="w-5 h-5 shrink-0 mt-0.5" />
                    <div>
                      <p className="font-bold">Error</p>
                      <p>{error}</p>
                    </div>
                  </div>
                )}

                <form onSubmit={handleSubmit} className="space-y-5">
                    <div>
                    <input 
                        type="text" 
                        value={username}
                        onChange={(e) => setUsername(e.target.value)}
                        className={`w-full px-4 py-3 bg-white border ${error ? 'border-red-300 bg-red-50' : 'border-slate-300'} rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent outline-none transition-all placeholder:text-slate-400`}
                        placeholder="Username"
                        required
                    />
                    </div>

                    <div>
                    <input 
                        type="password" 
                        value={password}
                        onChange={(e) => setPassword(e.target.value)}
                        className={`w-full px-4 py-3 bg-white border ${error ? 'border-red-300 bg-red-50' : 'border-slate-300'} rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent outline-none transition-all placeholder:text-slate-400`}
                        placeholder="Password"
                        required
                    />
                    </div>

                    <div className="flex items-center gap-2">
                        <input type="checkbox" id="saveUser" className="w-4 h-4 text-red-600 border-gray-300 rounded focus:ring-red-500" />
                        <label htmlFor="saveUser" className="text-sm text-slate-600">Save username</label>
                    </div>

                    <button 
                    type="submit" 
                    disabled={isLoading}
                    className={`w-full py-3 rounded-full font-bold text-white shadow-md transition-all transform active:scale-[0.98] ${
                        isLoading ? 'bg-red-400 cursor-not-allowed' : 'bg-red-600 hover:bg-red-700'
                    }`}
                    >
                    {isLoading ? 'Signing on...' : 'Sign On'}
                    </button>
                </form>

                <div className="mt-6 flex flex-col gap-3 text-center border-t border-slate-100 pt-6">
                    <a href="#" className="text-sm text-red-600 hover:underline font-medium">Forgot username or password?</a>
                    <a href="#" className="text-sm text-red-600 hover:underline font-medium">Enroll now</a>
                </div>
                </div>
                <div className="bg-slate-50 p-4 text-center border-t border-slate-100">
                    <p className="text-xs text-slate-500 flex items-center justify-center gap-1">
                        <Lock className="w-3 h-3" /> Secure System
                    </p>
                </div>
            </div>

            {/* Marketing/Info Side (Hidden on mobile) */}
            <div className="hidden md:block text-white pt-10">
                <h2 className="text-3xl font-bold mb-4 text-slate-800 drop-shadow-sm">Banking made easy.</h2>
                <p className="text-slate-700 text-lg mb-6 leading-relaxed">
                    Manage your accounts, pay bills, and transfer funds securely from anywhere with Canada Bank Online®.
                </p>
                <div className="bg-white/90 backdrop-blur-sm p-6 rounded-xl shadow-lg border border-white/50">
                    <h3 className="font-bold text-slate-900 mb-2 flex items-center gap-2">
                        <Shield className="w-5 h-5 text-emerald-600" /> Security Guarantee
                    </h3>
                    <p className="text-slate-600 text-sm">
                        We're committed to protecting your financial information. Learn more about how we keep you safe online.
                    </p>
                </div>
            </div>
        </div>
      </main>

      {/* Corporate Footer */}
      <footer className="bg-slate-900 text-slate-400 py-8 px-6 text-xs">
          <div className="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div className="flex gap-6">
                <a href="#" className="hover:text-white">Privacy, Cookies, Security & Legal</a>
                <a href="#" className="hover:text-white">Notice of Data Collection</a>
                <a href="#" className="hover:text-white">General Terms of Use</a>
            </div>
            <div className="text-center md:text-right">
                <p>© 1999 - 2024 Canada Bank. All rights reserved. NMLSR ID 399801</p>
                <p className="mt-1">Member FDIC. Equal Housing Lender.</p>
            </div>
          </div>
      </footer>
    </div>
  );
};

const Card = ({ account, onClick }) => (
  <div 
    onClick={() => onClick && onClick(account)}
    className={`relative overflow-hidden rounded-xl p-6 text-white shadow-lg bg-gradient-to-br ${account.color} transition-all hover:scale-[1.01] hover:shadow-xl duration-300 group cursor-pointer`}
  >
    <div className="absolute top-0 right-0 -mr-4 -mt-4 h-24 w-24 rounded-full bg-white opacity-10 blur-xl group-hover:opacity-20 transition-opacity"></div>
    <div className="relative z-10 flex flex-col justify-between h-full min-h-[150px]">
      <div className="flex justify-between items-start">
        <div>
          <p className="text-xs font-medium opacity-90 uppercase tracking-wider">{account.type}</p>
          <h3 className="text-lg font-bold mt-1 text-white">{account.name}</h3>
        </div>
        <div className="bg-white/20 p-2 rounded-lg backdrop-blur-sm">
            <CreditCard className="w-5 h-5 text-white" />
        </div>
      </div>
      
      <div className="mt-6">
        <div className="flex items-baseline gap-1">
            <span className="text-lg opacity-80">$</span>
            <p className="text-3xl font-bold tracking-tight">
            {Math.abs(account.balance).toLocaleString('en-US', { minimumFractionDigits: 2 })}
            </p>
        </div>
        <div className="flex justify-between items-end mt-4 pt-4 border-t border-white/10">
          <p className="text-xs opacity-80 font-mono tracking-widest">{account.number}</p>
          <span className="text-xs font-semibold bg-white/20 px-2 py-1 rounded text-white group-hover:bg-white group-hover:text-slate-900 transition-colors">Available</span>
        </div>
      </div>
    </div>
  </div>
);

const TransactionItem = ({ transaction }) => (
  <div className="flex items-center justify-between p-4 hover:bg-slate-50 rounded-lg transition-colors border-b border-slate-100 last:border-0 group cursor-pointer">
    <div className="flex items-center gap-4">
      <div className="h-10 w-10 rounded-full bg-slate-100 group-hover:bg-white group-hover:shadow-sm flex items-center justify-center text-xl transition-all">
        {transaction.icon}
      </div>
      <div>
        <h4 className="font-semibold text-slate-800 text-sm group-hover:text-red-700 transition-colors">{transaction.title}</h4>
        <p className="text-xs text-slate-500">{transaction.date} • {transaction.category}</p>
      </div>
    </div>
    <div className={`font-mono font-medium text-sm ${transaction.type === 'credit' ? 'text-emerald-700' : 'text-slate-700'}`}>
      {transaction.type === 'credit' ? '+' : '-'}${Math.abs(transaction.amount).toLocaleString('en-US', { minimumFractionDigits: 2 })}
    </div>
  </div>
);

// --- Main Application ---

export default function NexusBanking() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [activeTab, setActiveTab] = useState('dashboard');
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);
  const [data, setData] = useState(INITIAL_DATA);
  const [showBalance, setShowBalance] = useState(true);
  
  // Feature Specific States
  const [transferAmount, setTransferAmount] = useState('');
  const [transferTo, setTransferTo] = useState('');
  const [isProcessing, setIsProcessing] = useState(false);
  const [notification, setNotification] = useState(null);
  
  // Security Modal
  const [showSecurityModal, setShowSecurityModal] = useState(false);
  const [securityCode, setSecurityCode] = useState('');

  // Bill Pay State
  const [billPayee, setBillPayee] = useState('');
  const [billAmount, setBillAmount] = useState('');

  // Zelle State
  const [zelleContact, setZelleContact] = useState('');
  
  // Profile State
  const [isEditingProfile, setIsEditingProfile] = useState(false);
  const [tempProfile, setTempProfile] = useState({...data.user});

  const toggleMobileMenu = () => setIsMobileMenuOpen(!isMobileMenuOpen);
  const handleLogin = () => setIsLoggedIn(true);
  const handleLogout = () => { setIsLoggedIn(false); setActiveTab('dashboard'); setIsMobileMenuOpen(false); };

  // --- Handlers ---

  const showToast = (message, type = 'success') => {
    setNotification({ type, message });
    setTimeout(() => setNotification(null), 3000);
  };

  const initiateTransfer = (e) => {
    e.preventDefault();
    if (!transferAmount || parseFloat(transferAmount) <= 0 || !transferTo) return;
    setShowSecurityModal(true);
    setSecurityCode(''); 
  };

  const confirmTransfer = (e) => {
    e.preventDefault();
    if (securityCode !== '091996') return showToast('Invalid authentication code', 'error');

    setIsProcessing(true);
    setTimeout(() => {
      const amount = parseFloat(transferAmount);
      setData(prev => ({
        ...prev,
        accounts: prev.accounts.map(acc => acc.id === 1 ? { ...acc, balance: acc.balance - amount } : acc),
        transactions: [{ id: Date.now(), title: `Transfer to ${transferTo}`, date: "Just now", amount: -amount, type: "debit", category: "Transfer", icon: "💸" }, ...prev.transactions]
      }));
      setIsProcessing(false);
      setShowSecurityModal(false); 
      setTransferAmount('');
      setTransferTo('');
      showToast('Transfer successful!');
    }, 1500);
  };

  const handleBillPay = (e) => {
    e.preventDefault();
    if(!billPayee || !billAmount) return;
    setIsProcessing(true);
    setTimeout(() => {
        setData(prev => ({
            ...prev,
            accounts: prev.accounts.map(acc => acc.id === 1 ? { ...acc, balance: acc.balance - parseFloat(billAmount) } : acc),
            transactions: [{ id: Date.now(), title: `Bill Pay: ${data.payees.find(p => p.id === parseInt(billPayee))?.name}`, date: "Just now", amount: -parseFloat(billAmount), type: "debit", category: "Bill Pay", icon: "🧾" }, ...prev.transactions]
        }));
        setIsProcessing(false);
        setBillAmount('');
        setBillPayee('');
        showToast('Bill paid successfully!');
    }, 1000);
  };

  const handleZelleSend = (e) => {
    e.preventDefault();
    if(!zelleContact || !transferAmount) return;
    setIsProcessing(true);
    setTimeout(() => {
        setData(prev => ({
            ...prev,
            accounts: prev.accounts.map(acc => acc.id === 1 ? { ...acc, balance: acc.balance - parseFloat(transferAmount) } : acc),
            transactions: [{ id: Date.now(), title: `Zelle to ${zelleContact}`, date: "Just now", amount: -parseFloat(transferAmount), type: "debit", category: "Zelle", icon: "🟣" }, ...prev.transactions]
        }));
        setIsProcessing(false);
        setTransferAmount('');
        setZelleContact('');
        showToast(`Sent $${transferAmount} via Zelle®`);
    }, 1500);
  };

  const handleSaveProfile = () => {
      setData(prev => ({ ...prev, user: tempProfile }));
      setIsEditingProfile(false);
      showToast('Profile updated successfully');
  };

  // --- Components ---

  const NavItem = ({ id, icon: Icon, label }) => (
    <button
      onClick={() => { setActiveTab(id); setIsMobileMenuOpen(false); }}
      className={`w-full flex items-center gap-3 px-4 py-3 rounded-lg transition-all duration-200 text-sm ${
        activeTab === id 
          ? 'bg-red-600 text-white shadow-md' 
          : 'text-slate-600 hover:bg-slate-100 hover:text-slate-900'
      }`}
    >
      <Icon className="w-5 h-5" />
      <span className="font-medium">{label}</span>
      {activeTab === id && <ChevronRight className="w-4 h-4 ml-auto opacity-50" />}
    </button>
  );

  // --- Render Logic ---

  if (!isLoggedIn) return <LoginScreen onLogin={handleLogin} />;

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800 font-sans selection:bg-red-100 relative flex flex-col">
      
      {/* Notifications */}
      {notification && (
        <div className="fixed top-6 right-6 z-50 animate-bounce-in">
          <div className={`text-white px-6 py-4 rounded-lg shadow-xl flex items-center gap-3 ${notification.type === 'error' ? 'bg-red-600' : 'bg-emerald-600'}`}>
            <div className="bg-white/20 p-1 rounded-full">
              {notification.type === 'error' ? <X className="w-4 h-4" /> : <ArrowUpRight className="w-4 h-4" />}
            </div>
            <span className="font-medium">{notification.message}</span>
          </div>
        </div>
      )}

      {/* Security Modal */}
      {showSecurityModal && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm animate-fade-in">
          <div className="bg-white w-full max-w-md rounded-xl shadow-2xl overflow-hidden scale-100 animate-scale-in">
            <div className="p-6 text-center border-b border-slate-100">
              <div className="w-16 h-16 bg-red-50 rounded-full flex items-center justify-center mx-auto mb-4 border border-red-100">
                <Shield className="w-8 h-8 text-red-600" />
              </div>
              <h3 className="text-xl font-bold text-slate-900">Security Verification</h3>
              <p className="text-slate-500 text-sm mt-1">
                We sent a 6-digit code to <span className="font-mono text-slate-800">**89</span>
              </p>
            </div>
            
            <form onSubmit={confirmTransfer} className="p-6">
              <div className="mb-6">
                <label className="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-2 text-center">Enter Code</label>
                <div className="relative">
                  <KeyRound className="absolute left-4 top-1/2 -translate-y-1/2 w-5 h-5 text-slate-400" />
                  <input 
                    type="text" 
                    maxLength="6"
                    value={securityCode}
                    onChange={(e) => setSecurityCode(e.target.value.replace(/\D/g, ''))} // Only numbers
                    className="w-full pl-12 pr-4 py-4 bg-slate-50 border border-slate-200 rounded-xl text-center text-2xl font-mono tracking-[0.5em] focus:ring-2 focus:ring-red-500 focus:outline-none transition-all"
                    placeholder="000000"
                    autoFocus
                  />
                </div>
                <p className="text-center text-xs text-slate-400 mt-2">Tip: Use 091996</p>
              </div>

              <div className="flex gap-3">
                <button type="button" onClick={() => setShowSecurityModal(false)} className="flex-1 py-3 bg-slate-100 text-slate-700 font-bold rounded-lg hover:bg-slate-200">Cancel</button>
                <button type="submit" disabled={isProcessing} className="flex-1 py-3 bg-red-600 text-white font-bold rounded-lg hover:bg-red-700 shadow-lg shadow-red-200 disabled:opacity-50">{isProcessing ? 'Verifying...' : 'Verify'}</button>
              </div>
            </form>
          </div>
        </div>
      )}

      {/* Header */}
      <div className="bg-red-600 text-white text-xs py-1 px-4 hidden lg:flex justify-end gap-6">
          <a href="#" className="hover:underline">Personal</a>
          <a href="#" className="hover:underline opacity-80">Small Business</a>
          <a href="#" className="hover:underline opacity-80">Commercial</a>
      </div>
      <header className="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div className="max-w-7xl mx-auto px-4 lg:px-8 h-16 flex justify-between items-center">
             <div className="flex items-center gap-8">
                 <div className="flex items-center gap-2">
                    <div className="w-8 h-8 bg-red-600 rounded flex items-center justify-center text-white font-bold text-lg">C</div>
                    <span className="font-bold text-xl tracking-tight text-slate-900 hidden md:block">Canada Bank</span>
                 </div>
                 <nav className="hidden md:flex gap-6 text-sm font-medium text-slate-600">
                     <button onClick={() => setActiveTab('dashboard')} className={`${activeTab === 'dashboard' ? 'text-red-600 border-b-2 border-red-600' : 'hover:text-red-600'} py-5 transition-colors`}>Accounts</button>
                     <button onClick={() => setActiveTab('billpay')} className={`${activeTab === 'billpay' ? 'text-red-600 border-b-2 border-red-600' : 'hover:text-red-600'} py-5 transition-colors`}>Bill Pay</button>
                     <button onClick={() => setActiveTab('transfer')} className={`${activeTab === 'transfer' ? 'text-red-600 border-b-2 border-red-600' : 'hover:text-red-600'} py-5 transition-colors`}>Transfer</button>
                     <button onClick={() => setActiveTab('zelle')} className={`${activeTab === 'zelle' ? 'text-red-600 border-b-2 border-red-600' : 'hover:text-red-600'} py-5 transition-colors`}>Zelle®</button>
                 </nav>
             </div>
             <div className="flex items-center gap-4">
                 <button className="lg:hidden p-2" onClick={toggleMobileMenu}>{isMobileMenuOpen ? <X /> : <Menu />}</button>
                 <div className="hidden lg:flex items-center gap-3">
                     <button className="text-slate-500 hover:text-red-600"><Search className="w-5 h-5" /></button>
                     <button className="text-slate-500 hover:text-red-600"><Bell className="w-5 h-5" /></button>
                     <button onClick={handleLogout} className="text-xs font-bold text-slate-600 hover:text-red-600 border border-slate-300 px-3 py-1.5 rounded-full">Sign Off</button>
                 </div>
             </div>
        </div>
      </header>

      <div className="flex max-w-7xl mx-auto w-full flex-1 gap-6 p-4 lg:p-8">
        
        {/* Sidebar */}
        <aside className={`fixed inset-y-0 left-0 z-20 w-64 bg-white shadow-xl lg:shadow-none lg:bg-transparent transform transition-transform duration-300 lg:translate-x-0 lg:static lg:block ${isMobileMenuOpen ? 'translate-x-0' : '-translate-x-full'}`}>
          <div className="p-4 lg:p-0 h-full flex flex-col bg-white lg:bg-transparent rounded-lg">
            <div className="lg:hidden flex items-center justify-between mb-6">
                <span className="font-bold text-lg">Menu</span>
                <button onClick={toggleMobileMenu}><X className="w-5 h-5" /></button>
            </div>
            <div className="space-y-1">
              <NavItem id="dashboard" icon={Wallet} label="Account Summary" />
              <NavItem id="transactions" icon={FileText} label="Activity & Statements" />
              <NavItem id="transfer" icon={ArrowRightLeft} label="Transfer" />
              <NavItem id="billpay" icon={Building} label="Bill Pay" />
              <NavItem id="zelle" icon={Smartphone} label="Zelle®" />
              <div className="my-4 border-t border-slate-200"></div>
              <NavItem id="profile" icon={User} label="Profile & Settings" />
            </div>
            <div className="mt-8 bg-blue-50 p-4 rounded-xl border border-blue-100 hidden lg:block">
                <h4 className="font-bold text-blue-900 text-sm mb-2 flex items-center gap-2"><AlertCircle className="w-4 h-4" /> Security Alert</h4>
                <p className="text-xs text-blue-800 leading-relaxed">Review your contact info to ensure you receive fraud alerts.</p>
            </div>
          </div>
        </aside>

        {/* Main Content */}
        <main className="flex-1 w-full max-w-5xl">
            <div className="flex justify-between items-end mb-6">
                <div>
                    <h1 className="text-2xl font-bold text-slate-800">Good Morning, {data.user.name.split(' ')[0]}</h1>
                    <p className="text-slate-500 text-sm">Last sign on: {data.user.lastLogin}</p>
                </div>
                <button onClick={() => setShowBalance(!showBalance)} className="text-red-600 hover:text-red-800 flex items-center gap-2 text-sm font-medium bg-white px-3 py-1.5 rounded-full border border-slate-200 shadow-sm">
                    {showBalance ? <EyeOff className="w-4 h-4" /> : <Eye className="w-4 h-4" />}
                    {showBalance ? 'Hide Balances' : 'Show Balances'}
                </button>
            </div>

          {/* DASHBOARD */}
          {activeTab === 'dashboard' && (
            <div className="space-y-8 animate-fade-in">
               {/* Quick Actions */}
               <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                  {[
                      { icon: ArrowRightLeft, label: 'Transfer', tab: 'transfer' },
                      { icon: FileText, label: 'Bill Pay', tab: 'billpay' },
                      { icon: Smartphone, label: 'Zelle®', tab: 'zelle' },
                      { icon: Building, label: 'Statements', tab: 'transactions' }
                  ].map((action, i) => (
                      <button key={i} onClick={() => setActiveTab(action.tab)} className="flex flex-col items-center justify-center p-4 bg-white border border-slate-200 rounded-xl hover:border-red-400 hover:shadow-md transition-all group">
                          <div className="w-10 h-10 bg-slate-50 rounded-full flex items-center justify-center mb-2 group-hover:bg-red-50 group-hover:text-red-600 text-slate-600 transition-colors">
                              <action.icon className="w-5 h-5" />
                          </div>
                          <span className="text-xs font-bold text-slate-700">{action.label}</span>
                      </button>
                  ))}
              </div>

              {/* Accounts */}
              <section>
                <div className="flex justify-between items-center mb-4">
                  <h2 className="text-lg font-bold text-slate-800 flex items-center gap-2">Accounts</h2>
                </div>
                <div className="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
                  {data.accounts.map(account => (
                    <div key={account.id} className={showBalance ? '' : 'blur-sm select-none transition-all duration-500'}>
                      <Card 
                        account={account} 
                        onClick={(acc) => { if(acc.type === 'Credit') setActiveTab('cardDetail'); }} 
                      />
                    </div>
                  ))}
                </div>
              </section>

              {/* Transactions Preview */}
              <div className="bg-white rounded-xl shadow-sm border border-slate-200">
                <div className="p-4 border-b border-slate-100 flex justify-between items-center bg-slate-50/50 rounded-t-xl">
                    <h2 className="text-sm font-bold text-slate-800">Recent Transactions</h2>
                    <button onClick={() => setActiveTab('transactions')} className="text-xs text-red-600 font-bold hover:underline">View All</button>
                </div>
                <div>
                    {data.transactions.slice(0, 4).map(transaction => <TransactionItem key={transaction.id} transaction={transaction} />)}
                </div>
              </div>
            </div>
          )}

          {/* BILL PAY VIEW */}
          {activeTab === 'billpay' && (
            <div className="max-w-3xl mx-auto animate-fade-in">
                <h2 className="text-xl font-bold text-slate-800 mb-6">Pay Bills</h2>
                <div className="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
                    <div className="mb-8">
                        <label className="block text-sm font-bold text-slate-700 mb-3">Select Payee</label>
                        <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                            {data.payees.map(payee => (
                                <button 
                                    key={payee.id}
                                    onClick={() => setBillPayee(payee.id.toString())}
                                    className={`p-4 rounded-xl border-2 text-center transition-all ${billPayee === payee.id.toString() ? 'border-red-600 bg-red-50 text-red-700' : 'border-slate-100 hover:border-red-200'}`}
                                >
                                    <div className="w-10 h-10 mx-auto bg-white rounded-full shadow-sm flex items-center justify-center mb-2 font-bold text-slate-600">{payee.name.charAt(0)}</div>
                                    <div className="text-xs font-bold truncate">{payee.name}</div>
                                    <div className="text-[10px] text-slate-400 mt-1">Last: {payee.lastPaid}</div>
                                </button>
                            ))}
                            <button className="p-4 rounded-xl border-2 border-dashed border-slate-200 text-slate-400 flex flex-col items-center justify-center hover:bg-slate-50 hover:border-slate-300">
                                <span className="text-xl mb-1">+</span>
                                <span className="text-xs font-bold">Add Payee</span>
                            </button>
                        </div>
                    </div>

                    <form onSubmit={handleBillPay} className="space-y-6 max-w-md">
                         <div>
                            <label className="block text-sm font-medium text-slate-600 mb-2">Pay From</label>
                            <div className="flex items-center gap-3 p-3 bg-slate-50 rounded-lg border border-slate-200">
                                <Wallet className="w-5 h-5 text-slate-400" />
                                <div>
                                    <div className="text-sm font-bold">Everyday Checking</div>
                                    <div className="text-xs text-slate-500">Available: ${data.accounts[0].balance.toLocaleString()}</div>
                                </div>
                            </div>
                        </div>
                        <div>
                            <label className="block text-sm font-medium text-slate-600 mb-2">Amount</label>
                            <div className="relative">
                                <span className="absolute left-4 top-1/2 -translate-y-1/2 text-slate-500 font-bold">$</span>
                                <input 
                                    type="number" 
                                    value={billAmount}
                                    onChange={(e) => setBillAmount(e.target.value)}
                                    className="w-full pl-8 pr-4 py-3 bg-white border border-slate-200 rounded-lg focus:ring-2 focus:ring-red-600 outline-none font-bold text-lg"
                                    placeholder="0.00"
                                />
                            </div>
                        </div>
                        <button disabled={isProcessing || !billPayee} className="w-full py-4 bg-red-600 text-white font-bold rounded-lg hover:bg-red-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors">
                            {isProcessing ? 'Processing Payment...' : 'Pay Bill'}
                        </button>
                    </form>
                </div>
            </div>
          )}

          {/* ZELLE VIEW */}
          {activeTab === 'zelle' && (
            <div className="max-w-2xl mx-auto animate-fade-in">
                <div className="flex items-center gap-3 mb-6">
                    <div className="w-8 h-8 rounded bg-[#6d1ed4] flex items-center justify-center text-white font-bold">Z</div>
                    <h2 className="text-xl font-bold text-slate-800">Send Money with Zelle®</h2>
                </div>
                <div className="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
                    <div className="p-6 bg-[#f9f5fd] border-b border-purple-100 text-center">
                        <p className="text-purple-900 font-medium">Send money securely to friends and family.</p>
                    </div>
                    <form onSubmit={handleZelleSend} className="p-8 space-y-6">
                        <div>
                            <label className="block text-sm font-bold text-slate-700 mb-2">Recipient</label>
                            <div className="relative">
                                <Smartphone className="absolute left-4 top-1/2 -translate-y-1/2 w-5 h-5 text-slate-400" />
                                <input 
                                    type="text" 
                                    value={zelleContact}
                                    onChange={(e) => setZelleContact(e.target.value)}
                                    placeholder="Enter mobile number or email" 
                                    className="w-full pl-12 pr-4 py-4 bg-white border border-slate-200 rounded-xl focus:ring-2 focus:ring-[#6d1ed4] outline-none"
                                />
                            </div>
                        </div>
                        <div>
                             <label className="block text-sm font-bold text-slate-700 mb-2">Amount</label>
                             <div className="relative">
                                <span className="absolute left-4 top-1/2 -translate-y-1/2 text-slate-400 font-bold text-xl">$</span>
                                <input 
                                    type="number"
                                    value={transferAmount}
                                    onChange={(e) => setTransferAmount(e.target.value)}
                                    placeholder="0.00"
                                    className="w-full pl-10 pr-4 py-4 bg-white border border-slate-200 rounded-xl font-bold text-2xl focus:ring-2 focus:ring-[#6d1ed4] outline-none"
                                />
                             </div>
                        </div>
                        <button disabled={isProcessing} className="w-full py-4 bg-[#6d1ed4] text-white font-bold rounded-xl hover:bg-[#5a18b0] transition-colors shadow-lg shadow-purple-100">
                            {isProcessing ? 'Sending...' : 'Send with Zelle®'}
                        </button>
                    </form>
                </div>
            </div>
          )}

          {/* CARD DETAIL VIEW */}
          {activeTab === 'cardDetail' && (
            <div className="animate-fade-in space-y-6">
                <button onClick={() => setActiveTab('dashboard')} className="flex items-center gap-2 text-sm font-medium text-slate-500 hover:text-red-600 mb-4">
                    <ChevronRight className="w-4 h-4 rotate-180" /> Back to Dashboard
                </button>
                
                <div className="grid md:grid-cols-2 gap-8">
                    {/* Card Preview */}
                    <div>
                        <Card account={data.accounts[2]} />
                        <div className="mt-6 bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                            <h3 className="font-bold text-slate-800 mb-4">Rewards Status</h3>
                            <div className="flex items-end justify-between mb-2">
                                <span className="text-slate-500 text-sm">Cash Rewards Balance</span>
                                <span className="text-2xl font-bold text-emerald-600">${data.accounts[2].rewards.toFixed(2)}</span>
                            </div>
                            <div className="w-full bg-slate-100 rounded-full h-2 mb-4">
                                <div className="bg-emerald-500 h-2 rounded-full" style={{ width: '60%' }}></div>
                            </div>
                            <button className="w-full py-2 border border-slate-200 rounded-lg text-sm font-bold text-slate-600 hover:bg-slate-50">Redeem to Account</button>
                        </div>
                    </div>

                    {/* Stats */}
                    <div className="space-y-4">
                        <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-center justify-between">
                            <div>
                                <p className="text-xs font-bold text-slate-400 uppercase">Current APR</p>
                                <p className="text-xl font-bold text-slate-800">{data.accounts[2].apr}</p>
                            </div>
                            <Zap className="w-8 h-8 text-yellow-500 opacity-80" />
                        </div>
                        <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-center justify-between">
                            <div>
                                <p className="text-xs font-bold text-slate-400 uppercase">Payment Due</p>
                                <p className="text-xl font-bold text-red-600">{data.accounts[2].dueDate}</p>
                            </div>
                            <Calendar className="w-8 h-8 text-red-500 opacity-80" />
                        </div>
                        <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex items-center justify-between">
                            <div>
                                <p className="text-xs font-bold text-slate-400 uppercase">Credit Limit</p>
                                <p className="text-xl font-bold text-slate-800">${data.accounts[2].limit.toLocaleString()}</p>
                            </div>
                            <DollarSign className="w-8 h-8 text-slate-400 opacity-80" />
                        </div>
                    </div>
                </div>
            </div>
          )}

          {/* PROFILE VIEW */}
          {activeTab === 'profile' && (
            <div className="max-w-2xl mx-auto animate-fade-in">
                <div className="flex justify-between items-center mb-6">
                    <h2 className="text-xl font-bold text-slate-800">Profile & Settings</h2>
                    {!isEditingProfile ? (
                        <button onClick={() => setIsEditingProfile(true)} className="flex items-center gap-2 text-sm font-bold text-red-600 hover:bg-red-50 px-4 py-2 rounded-lg transition-colors">
                            <Edit2 className="w-4 h-4" /> Edit Profile
                        </button>
                    ) : (
                         <div className="flex gap-2">
                             <button onClick={() => { setIsEditingProfile(false); setTempProfile(data.user); }} className="text-sm font-bold text-slate-500 hover:bg-slate-100 px-4 py-2 rounded-lg">Cancel</button>
                             <button onClick={handleSaveProfile} className="text-sm font-bold text-white bg-red-600 hover:bg-red-700 px-4 py-2 rounded-lg shadow-sm">Save Changes</button>
                         </div>
                    )}
                </div>
                
                <div className="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
                    <div className="p-6 space-y-6">
                         <div className="flex items-center gap-6 pb-6 border-b border-slate-100">
                             <div className="w-20 h-20 bg-slate-100 rounded-full flex items-center justify-center text-2xl font-bold text-slate-400 border-4 border-white shadow-sm">
                                 {data.user.name.charAt(0)}
                             </div>
                             <div>
                                 <h3 className="text-lg font-bold text-slate-800">{data.user.name}</h3>
                                 <p className="text-slate-500 text-sm">Customer since 2018</p>
                             </div>
                         </div>

                         <div className="space-y-4">
                             <div>
                                 <label className="flex items-center gap-2 text-sm font-bold text-slate-700 mb-1"><Mail className="w-4 h-4 text-slate-400"/> Email Address</label>
                                 {isEditingProfile ? (
                                     <input type="email" value={tempProfile.email} onChange={(e) => setTempProfile({...tempProfile, email: e.target.value})} className="w-full p-3 border border-slate-200 rounded-lg outline-none focus:ring-2 focus:ring-red-600" />
                                 ) : <p className="p-3 bg-slate-50 rounded-lg text-slate-600">{data.user.email}</p>}
                             </div>
                             <div>
                                 <label className="flex items-center gap-2 text-sm font-bold text-slate-700 mb-1"><Phone className="w-4 h-4 text-slate-400"/> Phone Number</label>
                                 {isEditingProfile ? (
                                     <input type="text" value={tempProfile.phone} onChange={(e) => setTempProfile({...tempProfile, phone: e.target.value})} className="w-full p-3 border border-slate-200 rounded-lg outline-none focus:ring-2 focus:ring-red-600" />
                                 ) : <p className="p-3 bg-slate-50 rounded-lg text-slate-600">{data.user.phone}</p>}
                             </div>
                             <div>
                                 <label className="flex items-center gap-2 text-sm font-bold text-slate-700 mb-1"><MapPin className="w-4 h-4 text-slate-400"/> Address</label>
                                 {isEditingProfile ? (
                                     <input type="text" value={tempProfile.address} onChange={(e) => setTempProfile({...tempProfile, address: e.target.value})} className="w-full p-3 border border-slate-200 rounded-lg outline-none focus:ring-2 focus:ring-red-600" />
                                 ) : <p className="p-3 bg-slate-50 rounded-lg text-slate-600">{data.user.address}</p>}
                             </div>
                         </div>
                    </div>
                </div>
            </div>
          )}
          
          {/* TRANSFER VIEW (Original - Kept for fallback) */}
          {activeTab === 'transfer' && (
            <div className="max-w-2xl mx-auto animate-fade-in">
              <h2 className="text-xl font-bold text-slate-800 mb-4">Transfer Funds</h2>
              <div className="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
                    <form onSubmit={initiateTransfer}>
                    <div className="space-y-6">
                        <div>
                        <label className="block text-sm font-medium text-slate-700 mb-2">From Account</label>
                        <div className="p-4 border border-slate-200 rounded-lg flex items-center justify-between bg-white shadow-sm">
                            <div className="flex items-center gap-4">
                            <div className="w-10 h-10 rounded bg-red-50 flex items-center justify-center text-red-600"><Wallet className="w-5 h-5"/></div>
                            <div>
                                <p className="font-bold text-slate-800">Everyday Checking</p>
                                <p className="text-sm text-slate-500">Available: ${data.accounts[0].balance.toLocaleString()}</p>
                            </div>
                            </div>
                        </div>
                        </div>
                        <div>
                        <label className="block text-sm font-medium text-slate-700 mb-2">Recipient</label>
                        <input type="text" placeholder="Name, Email, or Account #" className="w-full p-4 bg-white border border-slate-200 rounded-lg focus:ring-2 focus:ring-red-600 outline-none" value={transferTo} onChange={(e) => setTransferTo(e.target.value)} />
                        </div>
                        <div>
                        <label className="block text-sm font-medium text-slate-700 mb-2">Amount</label>
                        <input type="number" placeholder="0.00" className="w-full p-4 bg-white border border-slate-200 rounded-lg font-bold text-xl focus:ring-2 focus:ring-red-600 outline-none" value={transferAmount} onChange={(e) => setTransferAmount(e.target.value)} />
                        </div>
                        <button type="submit" className="w-full py-4 rounded-lg font-bold text-lg text-white shadow-lg shadow-red-100 bg-red-600 hover:bg-red-700 transition-colors">Continue</button>
                    </div>
                    </form>
              </div>
            </div>
          )}

           {/* TRANSACTIONS VIEW */}
           {activeTab === 'transactions' && (
            <div className="space-y-6 animate-fade-in">
              <h2 className="text-xl font-bold text-slate-800">Activity & Statements</h2>
              <div className="bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
                <div className="p-4 border-b border-slate-200 flex gap-2 overflow-x-auto bg-slate-50">
                  {['All', 'Deposits', 'Withdrawals'].map((filter, i) => (
                    <button key={filter} className={`px-4 py-2 rounded-md text-sm font-medium whitespace-nowrap transition-colors ${i === 0 ? 'bg-white text-red-600 shadow-sm border border-slate-200' : 'text-slate-600 hover:text-slate-900'}`}>{filter}</button>
                  ))}
                </div>
                <div>
                  {data.transactions.map(transaction => <TransactionItem key={transaction.id} transaction={transaction} />)}
                </div>
              </div>
            </div>
          )}

        </main>
      </div>

      <footer className="bg-slate-100 text-slate-500 py-8 text-xs border-t border-slate-200 mt-auto">
            <div className="max-w-7xl mx-auto px-8 text-center">
                <p>Deposit products offered by Canada Bank. Member FDIC.</p>
                <p>© 1999 - 2024 Canada Bank. All rights reserved.</p>
            </div>
      </footer>
    </div>
  );
}
