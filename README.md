import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';

const currentUser = {
  name: 'Your Name',
  email: 'you@example.com',
  role: 'superadmin',
  score: 4400,
  medals: 4,
  followers: 397,
  following: 17,
  likes: 14870,
  coins: 115306,
};

const tasks = [
  { id: 1, title: 'Create a tech meme', reward: '100 pts + medal' },
  { id: 2, title: 'Write a beginner Python guide', reward: '200 pts + medal' },
];

const getBadge = (role) => {
  if (role === 'team') return '⭐';
  if (role === 'admin') return '⭐⭐';
  if (role === 'superadmin') return '⭐⭐⭐';
  return '';
};

function Home() {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-4">The People's Tech Community</h1>
      <p>Welcome, <strong>{currentUser.email}</strong> {getBadge(currentUser.role)}</p>

      {(currentUser.role === 'admin' || currentUser.role === 'superadmin') && (
        <div className="mt-6 p-4 bg-yellow-100 border-l-4 border-yellow-500">
          <h2 className="font-semibold">Admin Panel</h2>
          <ul className="list-disc ml-5">
            <li>📌 Pin/unpin posts</li>
            <li>🗑️ Delete posts</li>
            <li>📝 Assign tasks</li>
          </ul>
        </div>
      )}

      {currentUser.role === 'superadmin' && (
        <div className="mt-4 p-4 bg-blue-100 border-l-4 border-blue-500">
          <h2 className="font-semibold">Super Admin Controls</h2>
          <p>👑 Promote or remove admins</p>
        </div>
      )}
    </div>
  );
}

function Profile() {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">{currentUser.name}</h1>
      <p>{getBadge(currentUser.role)} {currentUser.role}</p>
      <p>{currentUser.email}</p>

      <div className="mt-4 space-y-1">
        <p>🎖️ Medals: {currentUser.medals}</p>
        <p>📈 Score: {currentUser.score}</p>
        <p>👥 Followers: {currentUser.followers}</p>
        <p>➡️ Following: {currentUser.following}</p>
        <p>❤️ Likes: {currentUser.likes}</p>
        <p>🪙 Coins: {currentUser.coins}</p>
      </div>
    </div>
  );
}

function Tasks() {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-4">Community Tasks</h1>
      {tasks.map(task => (
        <div key={task.id} className="bg-white p-4 shadow mb-4 rounded">
          <h2 className="text-lg font-semibold">{task.title}</h2>
          <p className="text-sm text-gray-500">Reward: {task.reward}</p>
          <button
            onClick={() => alert('Task submitted!')}
            className="mt-2 px-3 py-1 bg-blue-500 text-white rounded"
          >
            ✅ Mark as Complete
          </button>
        </div>
      ))}
    </div>
  );
}

export default function App() {
  return (
    <Router>
      <div className="min-h-screen bg-gray-100 text-gray-800">
        <nav className="bg-white shadow p-4 flex gap-4">
          <Link to="/" className="hover:underline">🏠 Home</Link>
          <Link to="/profile" className="hover:underline">👤 Profile</Link>
          <Link to="/tasks" className="hover:underline">📝 Tasks</Link>
        </nav>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/profile" element={<Profile />} />
          <Route path="/tasks" element={<Tasks />} />
        </Routes>
      </div>
    </Router>
  );
}
