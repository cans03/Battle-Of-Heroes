import { useState, useEffect } from "react";

export default function StrategyGame() {
  const [loading, setLoading] = useState(true);
  const [progress, setProgress] = useState(0);
  const [selectedRegion, setSelectedRegion] = useState(null);
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const [isAuth, setIsAuth] = useState(false);
  const [showRegisterOptions, setShowRegisterOptions] = useState(false);
  const [fullName, setFullName] = useState("");
  const [surname, setSurname] = useState("");
  const [birthDate, setBirthDate] = useState("");
  const [phoneNumber, setPhoneNumber] = useState("");
  const [newUsername, setNewUsername] = useState("");
  const [verificationSent, setVerificationSent] = useState(false);
  const [isAdmin, setIsAdmin] = useState(false);
  const [regionSelected, setRegionSelected] = useState(false);
  const [errorMessage, setErrorMessage] = useState("");
  const [showPhoneInput, setShowPhoneInput] = useState(false);
  const [showConstructionOptions, setShowConstructionOptions] = useState(false);

  useEffect(() => {
    let interval = setInterval(() => {
      setProgress((oldProgress) => {
        if (oldProgress >= 100) {
          clearInterval(interval);
          setLoading(false);
          return 100;
        }
        return oldProgress + 5;
      });
    }, 150);
    return () => clearInterval(interval);
  }, []);

  const handleRegister = () => {
    if (fullName && surname && birthDate && phoneNumber && newUsername) {
      setShowRegisterOptions(false);
      setUsername(newUsername);
      setPassword("");
    } else {
      setErrorMessage("Lütfen tüm bilgileri doldurun.");
    }
  };

  return (
    <div className="p-4 bg-gray-900 text-white min-h-screen flex flex-col items-center">
      <h1 className="text-3xl font-bold mb-4">Battle Of Heroes</h1>
      {!isLoggedIn ? (
        showRegisterOptions ? (
          <div className="flex flex-col gap-2 mb-4">
            <input 
              type="text" 
              placeholder="Ad" 
              className="px-2 py-1 rounded text-black" 
              value={fullName} 
              onChange={(e) => setFullName(e.target.value)} 
            />
            <input 
              type="text" 
              placeholder="Soyad" 
              className="px-2 py-1 rounded text-black" 
              value={surname} 
              onChange={(e) => setSurname(e.target.value)} 
            />
            <input 
              type="date" 
              placeholder="Doğum Tarihi" 
              className="px-2 py-1 rounded text-black" 
              value={birthDate} 
              onChange={(e) => setBirthDate(e.target.value)} 
            />
            <input 
              type="text" 
              placeholder="Telefon Numarası" 
              className="px-2 py-1 rounded text-black" 
              value={phoneNumber} 
              onChange={(e) => setPhoneNumber(e.target.value)} 
            />
            <input 
              type="text" 
              placeholder="Kullanıcı Adı" 
              className="px-2 py-1 rounded text-black" 
              value={newUsername} 
              onChange={(e) => setNewUsername(e.target.value)} 
            />
            <button className="px-4 py-2 bg-green-600 rounded-lg" onClick={handleRegister}>Kaydol</button>
            {errorMessage && <p className="text-red-500">{errorMessage}</p>}
          </div>
        ) : (
          <div className="flex flex-col gap-2 mb-4">
            <input 
              type="text" 
              placeholder="Kullanıcı Adı" 
              className="px-2 py-1 rounded text-black" 
              value={username} 
              onChange={(e) => setUsername(e.target.value)} 
            />
            <input 
              type="password" 
              placeholder="Şifre" 
              className="px-2 py-1 rounded text-black" 
              value={password} 
              onChange={(e) => setPassword(e.target.value)} 
            />
            <button className="text-blue-400 underline text-sm">Şifremi Unuttum</button>
            {errorMessage && <p className="text-red-500">{errorMessage}</p>}
            <button className="px-4 py-2 bg-blue-600 rounded-lg">Giriş Yap</button>
            <button className="px-4 py-2 bg-green-600 rounded-lg" onClick={() => setShowRegisterOptions(true)}>Kayıt Ol</button>
          </div>
        )
      ) : (
        <p>Oyuna giriş yapıldı.</p>
      )}
    </div>
  );
}
