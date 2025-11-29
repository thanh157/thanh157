import React, { useState, useEffect } from 'react';

const GitHubProfile = () => {
  const [leaves, setLeaves] = useState([]);

  useEffect(() => {
    const createLeaf = (id) => ({
      id,
      left: Math.random() * 100,
      animationDuration: 5 + Math.random() * 10,
      delay: Math.random() * 5,
      size: 15 + Math.random() * 15,
      rotation: Math.random() * 360,
      swing: Math.random() * 100 - 50
    });

    const initialLeaves = Array.from({ length: 20 }, (_, i) => createLeaf(i));
    setLeaves(initialLeaves);

    const interval = setInterval(() => {
      setLeaves(prev => {
        const newLeaves = [...prev];
        if (newLeaves.length < 30) {
          newLeaves.push(createLeaf(Date.now()));
        }
        return newLeaves.slice(-30);
      });
    }, 2000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="relative min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 overflow-hidden">
      {/* Hiệu ứng lá rơi */}
      {leaves.map((leaf) => (
        <div
          key={leaf.id}
          className="absolute pointer-events-none"
          style={{
            left: `${leaf.left}%`,
            top: '-50px',
            animation: `fall ${leaf.animationDuration}s linear infinite`,
            animationDelay: `${leaf.delay}s`,
            fontSize: `${leaf.size}px`,
            transform: `rotate(${leaf.rotation}deg)`,
            '--swing-amount': `${leaf.swing}px`
          }}
        >
          🍂
        </div>
      ))}

      {/* Nội dung chính */}
      <div className="relative z-10 flex flex-col items-center justify-center min-h-screen p-8">
        {/* Ảnh đại diện */}
        <div className="mb-8 relative">
          <div className="absolute inset-0 bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-500 rounded-full blur-xl opacity-50 animate-pulse"></div>
          <img
            src="https://i.pinimg.com/1200x/0a/30/15/0a301578fedbacc1db0274bece4384b9.jpg"
            alt="Profile"
            className="relative w-48 h-48 md:w-64 md:h-64 rounded-full object-cover border-4 border-white/30 shadow-2xl"
          />
        </div>

        {/* Tiêu đề */}
        <div className="text-center space-y-4 backdrop-blur-sm bg-white/5 p-8 rounded-2xl border border-white/10 shadow-2xl">
          <h1 className="text-4xl md:text-6xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-pink-400 via-purple-400 to-indigo-400 animate-pulse">
            ꧁Hello, Welcome to꧂
          </h1>
          <h2 className="text-3xl md:text-5xl font-bold text-white">
            Sad_girl.IT Github
          </h2>
          
          {/* Mô tả ngắn */}
          <p className="text-lg md:text-xl text-purple-200 max-w-2xl mx-auto mt-6">
            💻 Passionate Developer | 🌸 Creative Coder | ✨ Dream Builder
          </p>

          {/* Stats hoặc Skills */}
          <div className="flex flex-wrap justify-center gap-4 mt-8">
            {['JavaScript', 'React', 'Node.js', 'Python'].map((skill, i) => (
              <span
                key={i}
                className="px-4 py-2 bg-gradient-to-r from-pink-500/20 to-purple-500/20 border border-purple-400/30 rounded-full text-purple-200 text-sm font-medium backdrop-blur-sm hover:scale-110 transition-transform cursor-default"
              >
                {skill}
              </span>
            ))}
          </div>

          {/* Social Links */}
          <div className="flex justify-center gap-6 mt-8">
            <a href="#" className="text-3xl hover:scale-125 transition-transform">💌</a>
            <a href="#" className="text-3xl hover:scale-125 transition-transform">🌟</a>
            <a href="#" className="text-3xl hover:scale-125 transition-transform">🎨</a>
          </div>
        </div>

        {/* Quote */}
        <div className="mt-8 text-center">
          <p className="text-purple-300 italic text-lg">
            "Code with passion, create with heart 💜"
          </p>
        </div>
      </div>

      <style jsx>{`
        @keyframes fall {
          0% {
            transform: translateY(0) translateX(0) rotate(0deg);
          }
          100% {
            transform: translateY(100vh) translateX(var(--swing-amount)) rotate(360deg);
          }
        }
      `}</style>
    </div>
  );
};

export default GitHubProfile;
