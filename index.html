<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Shared Shopping List</title>
    
    <!-- React & Tailwind -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Firebase -->
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>

    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #f9fafb; }
        .tap-highlight-transparent { -webkit-tap-highlight-color: transparent; }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        // --- CONFIGURATION ---
        const firebaseConfig = {
          apiKey: "AIzaSyAHwMA5PZiF_zA_rapNTo7lDwOZKeJknWk",
          authDomain: "dummy-server-42e56.firebaseapp.com",
          projectId: "dummy-server-42e56",
          storageBucket: "dummy-server-42e56.firebasestorage.app",
          messagingSenderId: "926372732014",
          appId: "1:926372732014:web:9037bfd718d8ac69e41a7f",
          measurementId: "G-CDLWCP9T06"
        };

        // Initialize Firebase
        try {
            if (!firebase.apps.length) {
                firebase.initializeApp(firebaseConfig);
            }
        } catch (e) {
            document.body.innerHTML = `<div style="padding:20px; color:red">Firebase Init Error: ${e.message}</div>`;
        }
        
        const db = firebase.firestore();
        const auth = firebase.auth();

        const { useState, useEffect } = React;

        const ShoppingList = () => {
            const [user, setUser] = useState(null);
            const [items, setItems] = useState([]);
            const [newItem, setNewItem] = useState('');
            const [logs, setLogs] = useState(["Initializing app..."]);
            const [status, setStatus] = useState("connecting");

            const addLog = (msg) => setLogs(prev => [...prev, `${new Date().toLocaleTimeString()}: ${msg}`]);

            // 1. AUTHENTICATION
            useEffect(() => {
                addLog("Checking auth state...");
                const unsubscribe = auth.onAuthStateChanged(u => {
                    if (u) {
                        setUser(u);
                        addLog(`User authenticated: ${u.uid.slice(0,5)}...`);
                        setStatus("connected");
                    } else {
                        addLog("No user. Attempting Anonymous Sign-in...");
                        auth.signInAnonymously()
                            .then(() => addLog("Sign-in successful"))
                            .catch(err => {
                                addLog(`AUTH ERROR: ${err.message}`);
                                setStatus("error");
                                if(err.code === 'auth/operation-not-allowed') {
                                    alert("ENABLE ANONYMOUS AUTH: Go to Firebase Console -> Build -> Authentication -> Sign-in method -> Enable Anonymous.");
                                }
                            });
                    }
                });
                return () => unsubscribe();
            }, []);

            // 2. DATA SYNC
            useEffect(() => {
                if (!user) return;
                
                addLog("Connecting to Database...");
                const unsubscribe = db.collection('shopping-items')
                    .orderBy('createdAt', 'desc')
                    .onSnapshot(snapshot => {
                        const loaded = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                        loaded.sort((a, b) => (a.checked === b.checked ? 0 : a.checked ? 1 : -1));
                        setItems(loaded);
                        addLog(`Loaded ${loaded.length} items.`);
                    }, (err) => {
                        addLog(`DB ERROR: ${err.message}`);
                        setStatus("error");
                        if(err.code.includes("permission-denied")) {
                             alert("PERMISSION DENIED: Go to Firebase Console -> Build -> Firestore Database -> Rules. Change 'allow read, write: if false;' to 'allow read, write: if true;' (or enable Test Mode).");
                        }
                    });

                return () => unsubscribe();
            }, [user]);

            const addItem = async (e) => {
                e.preventDefault();
                if (!newItem.trim()) return;
                try {
                    await db.collection('shopping-items').add({
                        name: newItem.trim(),
                        checked: false,
                        createdAt: firebase.firestore.FieldValue.serverTimestamp()
                    });
                    setNewItem('');
                } catch (err) {
                    addLog(`Add Error: ${err.message}`);
                }
            };

            const toggleItem = async (item) => {
                try {
                    await db.collection('shopping-items').doc(item.id).update({ checked: !item.checked });
                } catch (err) {
                    addLog(`Update Error: ${err.message}`);
                }
            };

            const deleteItem = async (id) => {
                if(confirm('Delete?')) {
                    await db.collection('shopping-items').doc(id).delete();
                }
            };

            const seedData = async () => {
                const batch = db.batch();
                const ingredients = ["Method Granite cleaner", "Sugar", "Coffee", "Pie crusts", "Cascade Pods", "Apples (3.5 lbs)", "Lemon", "Brown Sugar", "Cornstarch", "Cinnamon", "Ginger", "Nutmeg", "Butter", "Flour"];
                ingredients.forEach(name => {
                    batch.set(db.collection('shopping-items').doc(), {
                        name, checked: false, createdAt: firebase.firestore.FieldValue.serverTimestamp()
                    });
                });
                await batch.commit();
            };

            const checkedCount = items.filter(i => i.checked).length;

            return (
                <div className="max-w-md mx-auto min-h-screen bg-gray-50 flex flex-col shadow-xl">
                    <div className={`${status === 'error' ? 'bg-red-600' : 'bg-emerald-600'} text-white p-4 sticky top-0 z-10 shadow-md`}>
                        <h1 className="font-bold text-xl">🛒 Shopping List</h1>
                        <div className="text-xs text-emerald-100 flex justify-between mt-2">
                            <span>{checkedCount}/{items.length} done</span>
                            <span>Status: {status.toUpperCase()}</span>
                        </div>
                    </div>

                    <div className="flex-1 overflow-y-auto p-4 pb-48 space-y-2">
                        {items.length === 0 && status === 'connected' && (
                             <button onClick={seedData} className="w-full py-4 text-emerald-600 font-bold border-2 border-dashed border-emerald-200 rounded-xl bg-emerald-50">
                                + Load Ingredients
                             </button>
                        )}

                        {items.map(item => (
                            <div key={item.id} onClick={() => toggleItem(item)} className={`flex items-center p-4 rounded-xl bg-white shadow-sm border ${item.checked ? 'bg-gray-50 opacity-60' : 'border-gray-100'}`}>
                                <div className={`w-6 h-6 rounded border-2 mr-3 flex items-center justify-center ${item.checked ? 'bg-emerald-500 border-emerald-500' : 'border-gray-300'}`}>
                                    {item.checked && <span className="text-white text-sm">✓</span>}
                                </div>
                                <span className={`flex-1 text-lg ${item.checked ? 'line-through text-gray-400' : ''}`}>{item.name}</span>
                                <button onClick={(e) => {e.stopPropagation(); deleteItem(item.id)}} className="p-2 text-gray-300">×</button>
                            </div>
                        ))}
                    </div>

                    {/* DEBUG LOG - VISIBLE ON SCREEN */}
                    <div className="bg-black text-green-400 p-4 font-mono text-xs h-32 overflow-y-auto border-t-4 border-gray-800">
                        <div className="font-bold text-white mb-1">--- DEBUG LOGS ---</div>
                        {logs.map((log, i) => <div key={i}>{log}</div>)}
                    </div>

                    <div className="fixed bottom-0 left-0 right-0 bg-white p-4 border-t border-gray-200 max-w-md mx-auto">
                        <form onSubmit={addItem} className="flex gap-2">
                            <input value={newItem} onChange={e => setNewItem(e.target.value)} placeholder="Add item..." className="flex-1 bg-gray-100 rounded-xl px-4 py-3 outline-none focus:ring-2 focus:ring-emerald-500" />
                            <button disabled={!newItem} className="bg-emerald-600 text-white w-14 rounded-xl font-bold text-2xl">+</button>
                        </form>
                    </div>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<ShoppingList />);
    </script>
</body>
</html>


