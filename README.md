// Frontend PWA – Controle de Estágios (Grau Técnico)
// Stack: React + Vite + TypeScript

// =======================
// src/main.tsx
// =======================
import React from 'react'
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'
import './styles/global.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
)

// =======================
// src/App.tsx
// =======================
import { Routes, Route, Navigate } from 'react-router-dom'
import Login from './pages/Login'
import DashboardAluno from './pages/aluno/DashboardAluno'
import DashboardPreceptor from './pages/preceptor/DashboardPreceptor'
import DashboardGestao from './pages/gestao/DashboardGestao'

export default function App() {
  return (
    <Routes>
      <Route path="/" element={<Login />} />
      <Route path="/aluno" element={<DashboardAluno />} />
      <Route path="/preceptor" element={<DashboardPreceptor />} />
      <Route path="/gestao" element={<DashboardGestao />} />
      <Route path="*" element={<Navigate to="/" />} />
    </Routes>
  )
}

// =======================
// src/pages/Login.tsx
// =======================
import { useState } from 'react'
import { useNavigate } from 'react-router-dom'

export default function Login() {
  const [matricula, setMatricula] = useState('')
  const [senha, setSenha] = useState('')
  const navigate = useNavigate()

  function handleLogin() {
    // Simulação de login
    if (matricula.startsWith('A')) navigate('/aluno')
    if (matricula.startsWith('P')) navigate('/preceptor')
    if (matricula.startsWith('G')) navigate('/gestao')
  }

  return (
    <div className="login-container">
      <h1>Grau Técnico</h1>
      <input placeholder="Matrícula" onChange={e => setMatricula(e.target.value)} />
      <input type="password" placeholder="Senha" onChange={e => setSenha(e.target.value)} />
      <button onClick={handleLogin}>Entrar</button>
    </div>
  )
}

// =======================
// src/pages/aluno/DashboardAluno.tsx
// =======================
export default function DashboardAluno() {
  return (
    <div className="page">
      <h2>Área do Aluno</h2>
      <button>Registrar Presença (QR-Code)</button>
      <button>Minhas Presenças</button>
    </div>
  )
}

// =======================
// src/pages/preceptor/DashboardPreceptor.tsx
// =======================
export default function DashboardPreceptor() {
  return (
    <div className="page">
      <h2>Área do Preceptor</h2>
      <button>Iniciar Sessão</button>
      <button>Encerrar Sessão</button>
      <div className="qr-box">QR-Code Dinâmico</div>
    </div>
  )
}

// =======================
// src/pages/gestao/DashboardGestao.tsx
// =======================
export default function DashboardGestao() {
  return (
    <div className="page">
      <h2>Gestão Acadêmica</h2>
      <ul>
        <li>Polos</li>
        <li>Grupos de Estágio</li>
        <li>Preceptores</li>
        <li>Relatórios</li>
      </ul>
    </div>
  )
}

// =======================
// src/styles/global.css
// =======================
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background: #f5f5f5;
}

.login-container, .page {
  max-width: 400px;
  margin: 80px auto;
  background: #fff;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

button {
  width: 100%;
  padding: 12px;
  margin-top: 12px;
  background: #003366;
  color: #fff;
  border: none;
  border-radius: 4px;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
}

.qr-box {
  margin-top: 20px;
  height: 200px;
  border: 2px dashed #003366;
  display: flex;
  align-items: center;
  justify-content: center;
}
