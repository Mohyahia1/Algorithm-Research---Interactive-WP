<!DOCTYPE html>
<html>
<head>
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-KF4N1CJWN9"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-KF4N1CJWN9');
</script>
  <title>Algorithm-Research---Interactive-WP</title>
  <!-- other head content -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Chosen Palette: Calm Harmony -->
  <!-- Application Structure Plan: ... -->
  <!-- Visualization & Content Choices: ... -->
  <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
  <title>ViaAlgo Explainer</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
      @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
      html { scroll-behavior: smooth; }
      body {
          background-color: #F8F7F4;
          color: #333333;
          font-family: 'Inter', sans-serif;
      }
      .fade-in-section {
          opacity: 0;
          transform: translateY(20px);
          transition: opacity 0.6s ease-out, transform 0.6s ease-out;
      }
      .fade-in-section.is-visible {
          opacity: 1;
          transform: translateY(0);
      }
      .sim-van {
          transition: all 2s ease-in-out;
          box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      }
      .sim-rider {
          transition: all 1s ease-in-out;
      }
      .path-line {
          transition: all 1.5s ease-in-out; /* Adjusted for height animation */
      }
      .sim-info-box {
          transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
      }
      .chart-container { 
          position: relative; 
          width: 100%; 
          max-width: 600px; 
          margin-left: auto; 
          margin-right: auto; 
          height: 300px;
          max-height: 400px; 
      }
      @media (min-width: 768px) { 
          .chart-container { height: 350px; } 
      }
  </style>
</head>
<body class="antialiased">

    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12">

        <!-- Responsive, larger header section -->
        <header class="text-center my-16 fade-in-section">
            <h1 class="text-5xl sm:text-6xl md:text-7xl lg:text-8xl font-extrabold text-[#333333] mb-4 tracking-tight">
                The Logic of the Ride
            </h1>
            <p class="text-2xl sm:text-3xl md:text-4xl font-semibold text-[#4A90E2] mb-2">
                Understanding Via's 'System-First' Algorithm
            </p>
            <p class="text-lg sm:text-xl md:text-2xl text-[#777] italic mt-3">
                A Research by Mohammed Majdi Alyahia
            </p>
        </header>

        <section class="my-24 fade-in-section">
            <div class="text-center max-w-3xl mx-auto">
                <h2 class="text-3xl font-bold mb-4 text-[#4A90E2]">
                    It’s Not About the Closest Car
                </h2>
                <p class="text-base md:text-lg leading-relaxed">
                    Via's algorithm doesn't just find the nearest vehicle. It performs a complex balancing act, making decisions that are best for the entire transportation network. It optimizes for overall efficiency, not just one person's convenience. This 'system-first' approach, operating like a dynamic 'virtual bus', is key to understanding why rides are assigned the way they are.
                </p>
            </div>
        </section>

        <section class="my-24 fade-in-section">
            <h2 class="text-3xl font-bold mb-8 text-center">
                The Algorithm's Balancing Act
            </h2>
            <p class="text-center max-w-3xl mx-auto mb-12">
                At its core, the algorithm constantly weighs several competing goals to find the most 'optimal' solution for the whole system. Hover over each goal to see the trade-off.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="group p-6 bg-white rounded-xl shadow-md text-center">
                    <div class="text-4xl mb-4">⚙️</div>
                    <h3 class="text-xl font-bold mb-2">Maximize Utilization</h3>
                    <p class="text-gray-600">Keep vehicles full and productive.</p>
                    <p class="mt-4 text-sm text-[#4A90E2] opacity-0 group-hover:opacity-100 transition-opacity">Trade-off: May lead to small detours for existing passengers.</p>
                </div>
                <div class="group p-6 bg-white rounded-xl shadow-md text-center">
                    <div class="text-4xl mb-4">⏱️</div>
                    <h3 class="text-xl font-bold mb-2">Minimize Wait Times</h3>
                    <p class="text-gray-600">Pick up riders as quickly as possible.</p>
                    <p class="mt-4 text-sm text-[#4A90E2] opacity-0 group-hover:opacity-100 transition-opacity">Trade-off: Might require dispatching a less-utilized vehicle.</p>
                </div>
                <div class="group p-6 bg-white rounded-xl shadow-md text-center">
                    <div class="text-4xl mb-4">💵</div>
                    <h3 class="text-xl font-bold mb-2">Reduce System Costs</h3>
                    <p class="text-gray-600">Minimize fuel and operational expenses.</p>
                    <p class="mt-4 text-sm text-[#4A90E2] opacity-0 group-hover:opacity-100 transition-opacity">Trade-off: The cheapest option might not be the fastest for a rider.</p>
                </div>
            </div>
        </section>
        
        <section class="my-24 fade-in-section">
            <h2 class="text-3xl font-bold mb-4 text-center">
                The 'Cost Function': The Algorithm's Brain
            </h2>
            <p class="text-center max-w-3xl mx-auto mb-8">
                The algorithm uses a 'cost function' to score every possible ride assignment. It adds up factors like delays and penalties for unserved rides. The assignment with the lowest total 'cost' wins. It even uses predictive analytics to position vehicles for future demand.
            </p>
            <div class="chart-container">
                <canvas id="costFunctionChart"></canvas>
            </div>
            <div class="text-center mt-6">
                <button id="toggleChartMode" class="bg-[#4A90E2] text-white font-bold py-2 px-6 rounded-lg shadow-md hover:bg-blue-600 transition-all">
                    Switch to 'High Demand' Mode
                </button>
            </div>
        </section>

        <section class="my-32 fade-in-section">
            <h2 class="text-3xl font-bold mb-4 text-center">
                Scenario 1: Utilized vs. Empty Van
            </h2>
            <p class="text-center max-w-3xl mx-auto mb-12">
                You request a ride and see two empty vans right in front of you. Why does the system assign your ride to a van that already has passengers? Let's see it in action.
            </p>

            <div class="bg-white rounded-xl shadow-lg p-4 md:p-8">
                <div class="flex flex-col md:flex-row gap-8">
                    <div class="w-full md:w-2/3 h-96 bg-gray-100 rounded-lg relative overflow-hidden" id="sim1-map">
                        <div id="sim1-rider" class="sim-rider absolute w-8 h-8 rounded-full bg-pink-500 border-2 border-white shadow-lg flex items-center justify-center" style="left: 50%; top: 80%; transform: translate(-50%, -50%);">🧍</div>
                        <div id="sim1-van1" class="sim-van absolute w-10 h-10 rounded-lg bg-blue-500 border-2 border-white flex items-center justify-center font-bold text-white" style="left: 20%; top: 60%;">1</div>
                        <div id="sim1-van2" class="sim-van absolute w-10 h-10 rounded-lg bg-blue-500 border-2 border-white flex items-center justify-center font-bold text-white" style="left: 80%; top: 60%;">2</div>
                        <div id="sim1-van3" class="sim-van absolute w-10 h-10 rounded-lg bg-green-500 border-2 border-white flex items-center justify-center font-bold text-white" style="left: 50%; top: 20%;">3</div>
                        <div id="sim1-path" class="path-line absolute bg-green-500 opacity-0" style="left: 50%; top: 20%; width: 2px; height: 0; transform: translateX(-50%);"></div>
                    </div>

                    <div class="w-full md:w-1/3">
                        <h3 class="text-xl font-bold mb-4">The System's Logic</h3>
                        <div id="sim1-initial" class="sim-info-box opacity-100">
                             <p class="text-sm mb-4">Van 1 & 2 are empty but are 'rebalancing' - moving strategically to meet predicted future demand. Van 3 is already active with a passenger.</p>
                            <button id="run-sim1" class="w-full bg-[#4A90E2] text-white font-bold py-3 px-6 rounded-lg shadow-md hover:bg-blue-600 transition-all">
                                Request Ride & See Why
                            </button>
                        </div>
                        <div id="sim1-result" class="sim-info-box opacity-0 absolute md:relative transform translate-y-4">
                           <div class="p-4 bg-green-100 border-l-4 border-green-500 rounded-r-lg">
                                <h4 class="font-bold text-green-800">Decision: Assign to Van 3</h4>
                                <p class="text-sm text-green-700">This is the lowest 'cost' option. Adding you to an active route is more efficient for the whole system (the 'virtual bus') than starting a new one or disrupting a rebalancing vehicle.</p>
                           </div>
                           <button id="reset-sim1" class="w-full mt-4 bg-gray-500 text-white font-bold py-2 px-4 rounded-lg hover:bg-gray-600 transition-all">
                                Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="my-32 fade-in-section">
            <h2 class="text-3xl font-bold mb-4 text-center">
                Scenario 2: Separate Vans for Separate Requests
            </h2>
            <p class="text-center max-w-3xl mx-auto mb-12">
                You and a friend request rides from nearby locations, but not at the exact same time. Why does the system put you in two different vans instead of pooling you together?
            </p>

            <div class="bg-white rounded-xl shadow-lg p-4 md:p-8">
                 <div class="flex flex-col md:flex-row gap-8">
                    <div class="w-full md:w-2/3 h-96 bg-gray-100 rounded-lg relative overflow-hidden" id="sim2-map">
                        <div id="sim2-rider1" class="sim-rider absolute w-8 h-8 rounded-full bg-pink-500 border-2 border-white shadow-lg flex items-center justify-center" style="left: 30%; top: 75%; transform: translate(-50%, -50%);">1️⃣</div>
                        <div id="sim2-rider2" class="sim-rider absolute w-8 h-8 rounded-full bg-purple-500 border-2 border-white shadow-lg flex items-center justify-center" style="left: 40%; top: 85%; transform: translate(-50%, -50%);">2️⃣</div>
                        <div id="sim2-vanA" class="sim-van absolute w-10 h-10 rounded-lg bg-teal-500 border-2 border-white flex items-center justify-center font-bold text-white" style="left: 20%; top: 20%;">A</div>
                        <div id="sim2-vanB" class="sim-van absolute w-10 h-10 rounded-lg bg-orange-500 border-2 border-white flex items-center justify-center font-bold text-white" style="left: 80%; top: 20%;">B</div>
                        <div id="sim2-pathA" class="path-line absolute bg-teal-500 opacity-0" style="left: 20%; top: 20%; width: 2px; height: 0; transform: translateX(-50%);"></div>
                        <div id="sim2-pathB" class="path-line absolute bg-orange-500 opacity-0" style="left: 80%; top: 20%; width: 2px; height: 0; transform: translateX(-50%);"></div>
                    </div>
                    
                    <div class="w-full md:w-1/3">
                        <h3 class="text-xl font-bold mb-4">The System's Logic</h3>
                        <div id="sim2-initial" class="sim-info-box opacity-100">
                             <p class="text-sm mb-4">Rider 1 requests a ride first. The system finds the optimal assignment. A moment later, Rider 2 makes a request.</p>
                            <button id="run-sim2-step1" class="w-full bg-teal-500 text-white font-bold py-3 px-6 rounded-lg shadow-md hover:bg-teal-600 transition-all">
                                1. Request for Rider 1
                            </button>
                        </div>
                        <div id="sim2-step2" class="sim-info-box opacity-0 absolute md:relative transform translate-y-4">
                           <div class="p-3 bg-teal-100 border-l-4 border-teal-500 rounded-r-lg mb-4">
                               <p class="text-sm text-teal-700">Van A is assigned to Rider 1. Its route is now optimized and committed.</p>
                           </div>
                           <button id="run-sim2-step2" class="w-full bg-orange-500 text-white font-bold py-3 px-6 rounded-lg shadow-md hover:bg-orange-600 transition-all">
                                2. Request for Rider 2
                            </button>
                        </div>
                         <div id="sim2-result" class="sim-info-box opacity-0 absolute md:relative transform translate-y-4">
                           <div class="p-3 bg-red-100 border-l-4 border-red-500 rounded-r-lg mb-2">
                                <h4 class="font-bold text-red-800">Analysis: Share with Van A?</h4>
                               <p class="text-sm text-red-700">Adding Rider 2 to Van A would violate constraints (e.g., cause a long delay for Rider 1). This is a high-cost option.</p>
                           </div>
                           <div class="p-3 bg-green-100 border-l-4 border-green-500 rounded-r-lg">
                                <h4 class="font-bold text-green-800">Decision: Assign to Van B</h4>
                               <p class="text-sm text-green-700">Assigning a separate van is the new optimal solution. It maintains service quality for both riders and is the lowest 'cost' choice for the system at this exact moment.</p>
                           </div>
                           <button id="reset-sim2" class="w-full mt-4 bg-gray-500 text-white font-bold py-2 px-4 rounded-lg hover:bg-gray-600 transition-all">
                                Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <footer class="text-center mt-32 pt-12 border-t border-gray-200 fade-in-section">
            <h2 class="text-3xl font-bold mb-4">
                Intelligence in Motion
            </h2>
            <p class="max-w-3xl mx-auto text-gray-600">
                Every ride assignment from Via is a calculated decision aimed at creating a more efficient, reliable, and sustainable transit system for everyone. It's a continuous, real-time optimization that balances the needs of individual riders with the health of the entire network.
            </p>
            <button 
              onclick="window.open('https://forms.gle/W1ExCCKkpurFKqsp9')" 
              class="mt-10 bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-lg shadow-lg transition-all text-lg flex items-center justify-center gap-2"
            >
              <svg class="w-6 h-6 mr-2" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M8 10h.01M12 10h.01M16 10h.01M21 12c0 3.866-3.582 7-8 7a8.966 8.966 0 0 1-4.9-1.467L3 19l1.528-3.43A6.978 6.978 0 0 1 3 12c0-3.866 3.582-7 8-7s8 3.134 8 7z" />
              </svg>
              Give me your feedback
            </button>
        </footer>

    </div>

<script>
/* ... rest of your JS unchanged ... */
</script>
</body>
</html>
