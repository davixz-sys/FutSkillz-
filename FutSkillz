import React, { useState, useEffect } from 'react';
import { User, Flame, TrendingUp, Zap, Dumbbell, Activity, Target, ChevronRight, Check, ArrowLeft, Camera, Play, Pause, RotateCcw } from 'lucide-react';

const FutSkillz = () => {
  const [screen, setScreen] = useState('welcome');
  const [userData, setUserData] = useState({
    age: '',
    weight: '',
    height: '',
    position: '',
    username: '',
    profilePic: null,
    email: '',
    subscriptionType: '',
    consecutiveDays: 0,
    trainingLevel: 'easy',
    lastTrainingDate: null,
    stats: {
      physical: 0,
      strength: 0,
      speed: 0,
      resistance: 0,
      technical: 0,
      positionSkill: 0
    }
  });
  
  const [selectedCategory, setSelectedCategory] = useState(null);
  const [selectedTraining, setSelectedTraining] = useState(null);
  const [timerRunning, setTimerRunning] = useState(false);
  const [timerSeconds, setTimerSeconds] = useState(0);
  const [googleConnected, setGoogleConnected] = useState(false);
  const [paymentMethod, setPaymentMethod] = useState('');
  const [cardData, setCardData] = useState({
    number: '',
    name: '',
    expiry: '',
    cvv: ''
  });
  const [pixData, setPixData] = useState({
    key: '',
    app: ''
  });

  // ===== DATA =====
  const positions = ['Atacante', 'Zagueiro', 'Lateral', 'Meio-campista', 'Goleiro'];
  
  const pixApps = [
    { id: 'nubank', name: 'Nubank', logo: '🟣' },
    { id: 'picpay', name: 'PicPay', logo: '💚' },
    { id: 'inter', name: 'Inter', logo: '🟠' },
    { id: 'c6', name: 'C6 Bank', logo: '⚫' },
    { id: 'neon', name: 'Neon', logo: '💙' },
    { id: 'next', name: 'Next', logo: '💚' },
    { id: 'mercadopago', name: 'Mercado Pago', logo: '💙' },
    { id: 'itau', name: 'Itaú', logo: '🟠' },
    { id: 'bradesco', name: 'Bradesco', logo: '🔴' },
    { id: 'santander', name: 'Santander', logo: '🔴' }
  ];

  const categories = [
    { id: 'technical', name: 'Técnico', icon: Target, color: 'from-white/20 to-white/10' },
    { id: 'strength', name: 'Força', icon: Dumbbell, color: 'from-white/20 to-white/10' },
    { id: 'physical', name: 'Físico', icon: Activity, color: 'from-white/20 to-white/10' },
    { id: 'position', name: 'Posição', icon: TrendingUp, color: 'from-white/20 to-white/10' },
    { id: 'speed', name: 'Velocidade', icon: Zap, color: 'from-white/20 to-white/10' }
  ];

  const trainings = {
    technical: [
      { 
        id: 1, name: 'Domínio Cruzado', description: 'Alternância de pés no controle de bola', duration: '5 min',
        steps: ['Posicione a bola à sua frente e prepare o pé direito', 'Toque a bola suavemente com a parte interna do pé direito', 'Imediatamente após, domine com a parte interna do pé esquerdo', 'Continue alternando os pés em ritmo constante por 30 segundos'],
        instructions: 'Este exercício desenvolve o domínio de bola com ambos os pés. Mantenha os joelhos levemente flexionados e olhe para a bola. O toque deve ser suave e controlado. Faça 3 séries de 30 segundos com 15 segundos de descanso entre elas.'
      },
      { 
        id: 2, name: 'Condução em Zigue-Zague', description: 'Dribles entre cones com mudança de direção', duration: '8 min',
        steps: ['Posicione 5 cones em linha reta com 2 metros de distância', 'Comece conduzindo a bola com a parte externa do pé direito', 'Ao chegar no cone, mude de direção usando a parte interna do pé', 'Alterne os pés a cada cone e retorne ao início'],
        instructions: 'Exercício fundamental para drible e mudança de direção. Mantenha a cabeça erguida e a bola próxima aos pés. Aumente a velocidade gradualmente conforme ganha confiança. Realize 5 repetições completas.'
      },
      { 
        id: 3, name: 'Passes Curtos Dinâmicos', description: 'Troca rápida de passes em dupla', duration: '10 min',
        steps: ['Fique a 5 metros de distância do seu parceiro', 'Passe a bola com a parte interna do pé direito', 'Receba o retorno posicionando o corpo de lado', 'Alterne entre pé direito e esquerdo a cada 5 passes'],
        instructions: 'Desenvolve precisão e velocidade nos passes. Concentre-se na parte interna do pé para maior controle. O corpo deve estar sempre de frente para o parceiro. Execute 3 séries de 20 passes (10 com cada pé).'
      }
    ],
    strength: [
      { 
        id: 1, name: 'Flexões Explosivas', description: 'Força de peitoral com impulso rápido', duration: '6 min',
        steps: ['Posição de prancha com mãos na largura dos ombros', 'Desça o corpo até o peito quase tocar o chão', 'Empurre explosivamente fazendo as mãos saírem do chão', 'Aterrisse suavemente e repita o movimento'],
        instructions: 'Fortalece peitoral, ombros e tríceps com explosão. Mantenha o core contraído e o corpo em linha reta. Se for muito difícil, comece com flexões normais. Faça 3 séries de 8-12 repetições.'
      },
      { 
        id: 2, name: 'Agachamento Isométrico', description: 'Força e resistência de pernas', duration: '4 min',
        steps: ['Fique de costas para a parede, pés afastados na largura dos ombros', 'Deslize as costas pela parede até formar 90° com os joelhos', 'Mantenha as costas retas e os braços estendidos à frente', 'Segure a posição por 30-60 segundos'],
        instructions: 'Desenvolve força e resistência nos quadríceps e glúteos. Os joelhos não devem ultrapassar a linha dos pés. Respire normalmente durante o exercício. Realize 3 séries de 45 segundos com 30 segundos de descanso.'
      },
      { 
        id: 3, name: 'Prancha Lateral', description: 'Core e estabilidade corporal', duration: '5 min',
        steps: ['Deite de lado apoiando o antebraço no chão', 'Empilhe os pés e eleve o quadril formando uma linha reta', 'Mantenha o corpo alinhado sem deixar o quadril cair', 'Segure por 30 segundos e troque de lado'],
        instructions: 'Fortalece oblíquos e melhora o equilíbrio. O cotovelo deve estar diretamente abaixo do ombro. Contraia o abdômen durante todo o exercício. Execute 3 séries de 30 segundos em cada lado.'
      }
    ],
    physical: [
      { 
        id: 1, name: 'Corrida Intervalada', description: '30s sprint + 30s caminhada, 10 vezes', duration: '15 min',
        steps: ['Aqueça com 3 minutos de trote leve', 'Corra em velocidade máxima por 30 segundos', 'Caminhe em ritmo moderado por 30 segundos para recuperar', 'Repita o ciclo 10 vezes e finalize com caminhada leve'],
        instructions: 'Melhora resistência cardiovascular e velocidade. Durante o sprint, dê tudo de si. Use a caminhada para recuperação ativa. Mantenha boa postura durante toda a corrida. Total: 10 minutos de treino.'
      },
      { 
        id: 2, name: 'Burpees Futebolísticos', description: 'Burpee + simulação de cabeceio', duration: '8 min',
        steps: ['Comece em pé, agache e apoie as mãos no chão', 'Jogue os pés para trás em posição de prancha', 'Retorne os pés para perto das mãos e salte para cima', 'No ponto máximo do salto, simule um cabeceio'],
        instructions: 'Exercício completo que trabalha corpo inteiro e explosão. Mantenha ritmo constante mas controlado. O salto final deve ser explosivo. Faça 3 séries de 10-15 repetições com 45 segundos de descanso.'
      },
      { 
        id: 3, name: 'Escada de Agilidade', description: 'Movimentação rápida entre marcações', duration: '7 min',
        steps: ['Marque 6 espaços no chão com 40cm de distância cada', 'Passe pelos espaços tocando 2 vezes em cada (direito-esquerdo)', 'Mantenha os joelhos altos e movimentos rápidos', 'Faça ida e volta sem parar'],
        instructions: 'Desenvolve coordenação, agilidade e velocidade de pés. Mantenha o corpo ligeiramente inclinado à frente. Os movimentos devem ser rápidos e precisos. Execute 5 repetições completas (ida e volta).'
      }
    ],
    position: [
      { 
        id: 1, name: 'Finalização em Área', description: 'Chutes de diferentes ângulos', duration: '12 min',
        steps: ['Posicione-se a 10 metros do gol (ou alvo)', 'Receba a bola vindo do lado direito e finalize de primeira', 'Repita recebendo do lado esquerdo', 'Alterne entre chutes rasteiros e elevados'],
        instructions: 'Treino específico para atacantes. Concentre-se na precisão antes da potência. O pé de apoio deve estar ao lado da bola. Olhe para o alvo antes de chutar. Faça 3 séries de 10 finalizações (5 de cada lado).'
      },
      { 
        id: 2, name: 'Marcação Pressão', description: 'Antecipação e bloqueio defensivo', duration: '10 min',
        steps: ['Posicione-se a 2 metros do atacante simulado', 'Quando ele receber a bola, aproxime-se rapidamente', 'Mantenha postura baixa e braços abertos', 'Force o adversário para o lado menos habilidoso'],
        instructions: 'Essencial para zagueiros e volantes. Mantenha distância segura mas pressione. Não se jogue no momento errado. Trabalhe em dupla para maior realismo. Pratique por 10 minutos alternando com parceiro.'
      },
      { 
        id: 3, name: 'Movimentação Sem Bola', description: 'Criação de espaços ofensivos', duration: '15 min',
        steps: ['Inicie em posição estática simulando marcação', 'Faça movimento de desmarque em diagonal', 'Acelere nos primeiros 3 passos para ganhar espaço', 'Olhe para quem está com a bola sinalizando o passe'],
        instructions: 'Fundamental para meio-campistas e atacantes. O timing do movimento é crucial. Varie entre diagonais e movimentos em profundidade. Treine com parceiro por 15 minutos fazendo 20 repetições.'
      }
    ],
    speed: [
      { 
        id: 1, name: 'Arrancada 10m', description: 'Explosão máxima em curta distância', duration: '10 min',
        steps: ['Posição inicial: uma perna à frente, corpo levemente inclinado', 'Ao sinal, exploda para frente com máxima aceleração', 'Mantenha passadas curtas e rápidas nos primeiros metros', 'Corra 10 metros em velocidade máxima'],
        instructions: 'Desenvolve explosão e aceleração inicial. Crucial para roubadas de bola e contra-ataques. Descanse 1 minuto entre cada arrancada. Realize 8 repetições focando em sair rápido da inércia.'
      },
      { 
        id: 2, name: 'Sprint com Mudança', description: 'Velocidade + troca rápida de direção', duration: '12 min',
        steps: ['Corra em linha reta por 5 metros em velocidade máxima', 'Ao chegar no cone, plante o pé externo e mude 90° à direita', 'Continue por mais 5 metros e mude novamente', 'Complete o quadrado retornando ao ponto inicial'],
        instructions: 'Combina velocidade com agilidade nas mudanças. Incline o corpo para o lado da mudança. Mantenha os joelhos flexionados. Faça 6 repetições completas alternando o sentido (horário/anti-horário).'
      },
      { 
        id: 3, name: 'Corrida Progressiva', description: 'Aceleração gradual até velocidade máxima', duration: '11 min',
        steps: ['Comece trotando leve nos primeiros 10 metros', 'Aumente para 70% da velocidade nos próximos 10 metros', 'Acelere para 90% nos próximos 10 metros', 'Finalize com máxima velocidade nos últimos 10 metros'],
        instructions: 'Treina controle de velocidade e aceleração progressiva. Importante para contra-ataques organizados. Descanse 90 segundos entre cada corrida. Execute 5 repetições mantendo controle em cada fase.'
      }
    ]
  };

  // Save/Load from localStorage
  useEffect(() => {
    try {
      localStorage.setItem('futskillz_user', JSON.stringify(userData));
    } catch (e) {}
  }, [userData]);

  useEffect(() => {
    try {
      const saved = localStorage.getItem('futskillz_user');
      if (saved) {
        setUserData(prev => ({ ...prev, ...JSON.parse(saved) }));
      }
    } catch (e) {}
  }, []);

  // Timer
  useEffect(() => {
    let interval = null;
    if (timerRunning) {
      interval = setInterval(() => {
        setTimerSeconds(s => s + 1);
      }, 1000);
    }
    return () => clearInterval(interval);
  }, [timerRunning]);

  // ===== UTILITY FUNCTIONS =====
  const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60);
    const secs = seconds % 60;
    return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
  };

  const resetTimer = () => {
    setTimerSeconds(0);
    setTimerRunning(false);
  };

  const calculateIdealWeight = (height) => {
    const h = height / 100;
    return { 
      min: (18.5 * h ** 2).toFixed(1), 
      max: (24.9 * h ** 2).toFixed(1) 
    };
  };

  const getWeightStatus = () => {
    if (!userData.weight || !userData.height) return null;
    const ideal = calculateIdealWeight(userData.height);
    if (userData.weight < ideal.min) return { status: 'abaixo', text: 'Abaixo do peso ideal' };
    if (userData.weight > ideal.max) return { status: 'acima', text: 'Acima do peso ideal' };
    return { status: 'ideal', text: 'Peso ideal' };
  };

  const getWeightPercentage = () => {
    if (!userData.weight || !userData.height) return 0;
    const ideal = calculateIdealWeight(userData.height);
    const idealMid = (parseFloat(ideal.min) + parseFloat(ideal.max)) / 2;
    const diff = Math.abs(userData.weight - idealMid);
    const maxDiff = idealMid * 0.3;
    return Math.max(0, Math.min(100, 100 - (diff / maxDiff) * 100)).toFixed(0);
  };

  const getWeightProgress = () => {
    if (!userData.weight || !userData.height) return { toIdeal: '0 kg', percentage: 0 };
    const ideal = calculateIdealWeight(userData.height);
    const idealMid = (parseFloat(ideal.min) + parseFloat(ideal.max)) / 2;
    const diff = userData.weight - idealMid;
    const percentage = getWeightPercentage();
    
    if (Math.abs(diff) < 1) return { toIdeal: 'Peso ideal alcançado! 🎉', percentage: 100 };
    else if (diff > 0) return { toIdeal: `${Math.abs(diff).toFixed(1)} kg para perder`, percentage: parseInt(percentage) };
    else return { toIdeal: `${Math.abs(diff).toFixed(1)} kg para ganhar`, percentage: parseInt(percentage) };
  };

  const getOverallEvolution = () => {
    const stats = userData.stats;
    return ((stats.physical + stats.strength + stats.speed + stats.technical + stats.positionSkill) / 5).toFixed(0);
  };

  const getFlameColor = (days) => {
    if (days >= 61) return 'text-blue-400';
    if (days >= 41) return 'text-purple-400';
    if (days >= 21) return 'text-red-500';
    return 'text-orange-500';
  };

  const getPositionStats = () => {
    const positionMap = {
      'Atacante': [
        { name: 'Finalização', value: userData.stats.positionSkill || 0 },
        { name: 'Condução de Bola', value: userData.stats.technical || 0 },
        { name: 'Drible', value: userData.stats.technical || 0 }
      ],
      'Zagueiro': [
        { name: 'Defesa', value: userData.stats.positionSkill || 0 },
        { name: 'Marcação', value: userData.stats.strength || 0 },
        { name: 'Jogo Aéreo', value: userData.stats.strength || 0 }
      ],
      'Lateral': [
        { name: 'Velocidade', value: userData.stats.speed || 0 },
        { name: 'Cruzamento', value: userData.stats.technical || 0 },
        { name: 'Cobertura', value: userData.stats.physical || 0 }
      ],
      'Meio-campista': [
        { name: 'Passes', value: userData.stats.technical || 0 },
        { name: 'Visão de Jogo', value: userData.stats.positionSkill || 0 },
        { name: 'Resistência', value: userData.stats.physical || 0 }
      ],
      'Goleiro': [
        { name: 'Reflexos', value: userData.stats.positionSkill || 0 },
        { name: 'Posicionamento', value: userData.stats.technical || 0 },
        { name: 'Saída de Gol', value: userData.stats.speed || 0 }
      ]
    };
    return positionMap[userData.position] || [];
  };

  const handleProfilePicChange = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => setUserData({...userData, profilePic: reader.result});
      reader.readAsDataURL(file);
    }
  };

  const handleGoogleConnect = () => {
    setGoogleConnected(true);
    setUserData(prev => ({
      ...prev,
      username: 'João Silva',
      email: 'joao.silva@gmail.com',
      profilePic: 'https://ui-avatars.com/api/?name=Joao+Silva&background=ffffff&color=000&size=200'
    }));
  };

  // ===== WELCOME SCREEN =====
  if (screen === 'welcome') {
    return (
      <div className="min-h-screen bg-black flex items-center justify-center p-4 relative overflow-hidden">
        <div 
          className="absolute inset-0 opacity-10"
          style={{
            backgroundImage: 'linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px)',
            backgroundSize: '50px 50px'
          }}
        />

        <div className="relative z-10 w-full max-w-md">
          <div className="bg-gradient-to-b from-gray-800/30 to-gray-900/30 rounded-[3rem] p-4 border-4 border-gray-700/50 shadow-2xl">
            <div className="bg-black rounded-[2.5rem] overflow-hidden border border-gray-800">
              <div className="px-8 py-12 flex flex-col items-center">
                <div className="flex items-center justify-center mb-8">
                  <span className="text-5xl mr-3">⚽</span>
                  <h1 className="text-5xl font-bold text-white tracking-wider">FUTSKILLZ</h1>
                </div>

                <div className="my-8 relative">
                  <img 
                    src="https://i.postimg.cc/VNXQqQQF/soccer-player.png" 
                    alt="Soccer Player"
                    className="w-72 h-auto mx-auto"
                    style={{ filter: 'drop-shadow(0 0 40px rgba(255,255,255,0.15))' }}
                  />
                  <div className="absolute -top-4 -right-4 w-12 h-12">
                    <span className="text-4xl">⚽</span>
                  </div>
                </div>

                <h2 className="text-3xl font-bold text-white mb-8 tracking-widest">SOCCER TRAINING</h2>

                <button
                  onClick={() => setScreen('questionnaire')}
                  className="w-full bg-transparent border-3 border-white text-white px-12 py-5 rounded-full font-bold text-2xl tracking-wider hover:bg-white hover:text-black transition-all duration-300 shadow-lg"
                >
                  START
                </button>

                <div className="flex items-center justify-center space-x-16 mt-12 opacity-40">
                  <User className="w-8 h-8 text-gray-400" />
                  <Activity className="w-8 h-8 text-gray-400" />
                  <Target className="w-8 h-8 text-gray-400" />
                </div>
              </div>
            </div>
          </div>
        </div>

        <div className="absolute top-0 left-0 w-40 h-40 border-l-2 border-t-2 border-orange-500/30" />
        <div className="absolute top-0 right-0 w-40 h-40 border-r-2 border-t-2 border-orange-500/30" />
        <div className="absolute bottom-0 left-0 w-40 h-40 border-l-2 border-b-2 border-orange-500/30" />
        <div className="absolute bottom-0 right-0 w-40 h-40 border-r-2 border-b-2 border-orange-500/30" />
      </div>
    );
  }

  // ===== QUESTIONNAIRE =====
  if (screen === 'questionnaire') {
    const weightStatus = getWeightStatus();
    return (
      <div className="min-h-screen bg-black p-6">
        <div className="max-w-md mx-auto">
          <h2 className="text-3xl font-bold text-white mb-8">Criar Perfil</h2>
          
          <div className="space-y-6">
            <div>
              <label className="text-gray-300 block mb-2">Idade</label>
              <input
                type="number"
                value={userData.age}
                onChange={(e) => setUserData({...userData, age: e.target.value})}
                className="w-full bg-white/5 border border-white/10 text-white px-4 py-3 rounded-xl focus:outline-none focus:border-white/30 transition"
                placeholder="Ex: 18"
              />
            </div>

            <div>
              <label className="text-gray-300 block mb-2">Peso (kg)</label>
              <input
                type
