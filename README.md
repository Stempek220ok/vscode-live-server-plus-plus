<!doctype html>
<html lang="pl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>react app na telefonie</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<body class="bg-gray-100 flex items-center justify-center h-screen">
<div id="root" class="w-full max-w-md"></div>
<script type="text/babel">
    const { useState } = React; // Corrected usestate to useState

    // --- ekran: główny ---
    function HomeScreen({ onNavigate }) {
        return (
            <div className="p-6 bg-white rounded-lg shadow-md animate-fade-in">
                <h1 className="text-3xl font-bold mb-4 text-gray-800">główny ekran</h1>
                <p className="text-gray-700 mb-6">witaj na ekranie głównym! to jest treść strony głównej.</p>
                <button onClick={() => onNavigate('settings')} className="px-5 py-2 mr-2 bg-blue-600 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-all duration-200" >
                    idź do ustawień
                </button>
                <button onClick={() => onNavigate('gemini')} className="px-5 py-2 bg-green-600 text-white font-semibold rounded-lg shadow-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 transition-all duration-200" >
                    przejdź do chatu ai
                </button>
            </div>
        );
    }

    // --- ekran: ustawienia ---
    function SettingsScreen({ onNavigate }) {
        return (
            <div className="p-6 bg-white rounded-lg shadow-md animate-fade-in">
                <h1 className="text-3xl font-bold mb-4 text-gray-800">ustawienia (tylko ty)</h1>
                <p className="text-gray-700 mb-6">tutaj znajdują się twoje prywatne ustawienia.</p>
                {/* Added a back button to navigate home */}
                <button onClick={() => onNavigate('home')} className="px-5 py-2 bg-gray-600 text-white font-semibold rounded-lg shadow-md hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-gray-500 transition-all duration-200" >
                    wróć do głównego ekranu
                </button>
            </div>
        );
    }
    
    // --- ekran: chat ai (dodany dla kompletności) ---
    function GeminiScreen({ onNavigate }) {
        return (
            <div className="p-6 bg-white rounded-lg shadow-md animate-fade-in">
                <h1 className="text-3xl font-bold mb-4 text-gray-800">chat ai</h1>
                <p className="text-gray-700 mb-6">tutaj możesz rozmawiać z AI.</p>
                <button onClick={() => onNavigate('home')} className="px-5 py-2 bg-gray-600 text-white font-semibold rounded-lg shadow-md hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-gray-500 transition-all duration-200" >
                    wróć do głównego ekranu
                </button>
            </div>
        );
    }

    // --- główny komponent aplikacji z routingiem ---
    function App() {
        const [screen, setScreen] = useState('home');

        const navigateTo = (screenName) => {
            setScreen(screenName);
        };

        const renderScreen = () => {
            switch (screen) {
                case 'home':
                    return <HomeScreen onNavigate={navigateTo} />;
                case 'settings':
                    return <SettingsScreen onNavigate={navigateTo} />;
                case 'gemini':
                    return <GeminiScreen onNavigate={navigateTo} />;
                default:
                    return <HomeScreen onNavigate={navigateTo} />;
            }
        };

        return (
            <div className="container mx-auto p-4">
                {renderScreen()}
            </div>
        );
    }

    // Renderowanie aplikacji do elementu root
    ReactDOM.render(<App />, document.getElementById('root'));
</script>
</body>
</html>
