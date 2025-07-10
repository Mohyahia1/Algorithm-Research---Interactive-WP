<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Chosen Palette: Calm Harmony -->
    <!-- Application Structure Plan: A single-page, "scrollytelling" application. The structure is designed to guide the user from high-level concepts to specific, interactive examples. It starts with the core idea (System-First Optimization), visualizes the algorithm's competing goals and its "brain" (The Cost Function), and then lets users engage with two interactive scenarios that directly answer the core user questions. This thematic, interactive flow is more intuitive for learning than a traditional report layout, transforming passive reading into active exploration and understanding. -->
    <!-- Visualization & Content Choices: 
        - Report Info: Multi-objective optimization (utilization, wait times, costs). Goal: Inform/Compare. Viz: Interactive HTML diagram with hover effects showing conflicting goals. Interaction: Hover to see trade-offs. Justification: Makes an abstract concept tangible. Method: HTML/CSS/JS.
        - Report Info: Cost function components and their changing priorities. Goal: Inform/Organize. Viz: Dynamic Chart.js Bar Chart. Interaction: A button toggles the chart between 'Standard' and 'High Demand' modes to see how priorities shift. Justification: Quantifies priorities and shows the system's adaptability. Method: Chart.js.
        - Report Info: Scenario 1 (Utilized vs. Empty Van). Goal: Explain a complex process visually. Viz: Animated map-like simulation. Interaction: User-triggered animation with tooltips explaining vehicle status (e.g., "Rebalancing for future demand"). Justification: A visual story is more effective than text for this spatial logic. Method: HTML/CSS/JS.
        - Report Info: Scenario 2 (Separate Vans for non-simultaneous requests). Goal: Show cause-and-effect over time. Viz: Two-step animated map simulation. Interaction: Staged button clicks to show how timing changes the optimal solution, with visual cues for "Constraint Violated!". Justification: Clearly demonstrates the time-sensitive, dynamic nature of the algorithm. Method: HTML/CSS/JS.
    -->
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

        <header class="text-center my-16 fade-in-section">
            <h1 class="text-4xl md:text-6xl font-bold text-[#333333] mb-4">
                The Logic of the Ride
            </h1>
            <p class="text-lg md:text-xl text-[#555]">
                Understanding Via's 'System-First' Algorithm
            </p>
            <p class="text-base md:text-lg text-[#777] mt-2">
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
        </footer>

    </div>

<script>
document.addEventListener('DOMContentLoaded', () => {

    const translations = {
        "Switch to 'High Demand' Mode": "Switch to 'High Demand' Mode",
        "Switch to 'Standard' Mode": "Switch to 'Standard' Mode",
        "Unassigned Ride Penalty": "Unassigned Ride Penalty",
        "Vehicle Utilization": "Vehicle Utilization",
        "Passenger Wait Time": "Passenger Wait Time",
        "Passenger Travel Delay": "Passenger Travel Delay",
        "Operational Costs": "Operational Costs",
        "Cost / Importance": "Cost / Importance"
    };

    const sections = document.querySelectorAll('.fade-in-section');
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('is-visible');
            }
        });
    }, { threshold: 0.1 });

    sections.forEach(section => {
        observer.observe(section);
    });
    
    const ctx = document.getElementById('costFunctionChart').getContext('2d');
    const chartToggleButton = document.getElementById('toggleChartMode');
    let isHighDemandMode = false;

    const chartData = {
        standard: [8, 9, 6, 5, 7],
        highDemand: [10, 6, 8, 4, 9]
    };
    
    const labels = [
        translations["Unassigned Ride Penalty"], 
        translations["Vehicle Utilization"], 
        translations["Passenger Wait Time"], 
        translations["Passenger Travel Delay"],
        translations["Operational Costs"]
    ];

    window.costChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: labels,
            datasets: [{
                label: translations["Cost / Importance"],
                data: chartData.standard,
                backgroundColor: [
                    'rgba(255, 99, 132, 0.5)',
                    'rgba(54, 162, 235, 0.5)',
                    'rgba(255, 206, 86, 0.5)',
                    'rgba(75, 192, 192, 0.5)',
                    'rgba(153, 102, 255, 0.5)'
                ],
                borderColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            indexAxis: 'y',
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    display: false
                },
                tooltip: {
                    callbacks: {
                        label: function(context) {
                            let label = context.dataset.label || '';
                            if (label) {
                                label += ': ';
                            }
                            if (context.parsed.x !== null) {
                                label += context.parsed.x;
                            }
                            return label;
                        }
                    }
                }
            },
            scales: {
                x: {
                    beginAtZero: true,
                    title: {
                        display: true,
                        text: translations["Cost / Importance"]
                    }
                }
            }
        }
    });
    
    function updateChartLanguage() {
        costChart.data.labels = labels;
        costChart.options.scales.x.title.text = translations["Cost / Importance"];
        costChart.data.datasets[0].label = translations["Cost / Importance"];
        chartToggleButton.innerText = isHighDemandMode ? translations["Switch to 'Standard' Mode"] : translations["Switch to 'High Demand' Mode"];
        costChart.update();
    }
    
    chartToggleButton.addEventListener('click', () => {
        isHighDemandMode = !isHighDemandMode;
        costChart.data.datasets[0].data = isHighDemandMode ? chartData.highDemand : chartData.standard;
        updateChartLanguage();
    });

    const runSim1Btn = document.getElementById('run-sim1');
    const resetSim1Btn = document.getElementById('reset-sim1');
    const sim1Van3 = document.getElementById('sim1-van3');
    const sim1Path = document.getElementById('sim1-path');
    const sim1Initial = document.getElementById('sim1-initial');
    const sim1Result = document.getElementById('sim1-result');

    const sim1InitialState = {
        van3: { left: '50%', top: '20%' },
        path: { opacity: '0', height: '0', top: '20%', width: '2px', transform: 'translateX(-50%)' } 
    };

    function runSim1() {
        runSim1Btn.disabled = true;
        
        sim1Path.style.opacity = sim1InitialState.path.opacity;
        sim1Path.style.height = sim1InitialState.path.height;
        sim1Path.style.top = sim1InitialState.path.top;
        sim1Path.style.width = sim1InitialState.path.width;
        sim1Path.style.transform = sim1InitialState.path.transform;

        setTimeout(() => {
            sim1Path.style.opacity = '1';
            sim1Path.style.height = '60%'; 
        }, 100); 

        setTimeout(() => {
            sim1Van3.style.top = '80%'; 
        }, 1500); 

        setTimeout(() => {
            sim1Initial.classList.remove('opacity-100');
            sim1Initial.classList.add('opacity-0', 'absolute');
            sim1Result.classList.remove('opacity-0', 'absolute');
            sim1Result.classList.add('opacity-100');
        }, 3500); 
    }

    function resetSim1() {
        runSim1Btn.disabled = false;
        sim1Van3.style.left = sim1InitialState.van3.left;
        sim1Van3.style.top = sim1InitialState.van3.top;
        
        sim1Path.style.opacity = sim1InitialState.path.opacity;
        sim1Path.style.height = sim1InitialState.path.height;
        sim1Path.style.top = sim1InitialState.path.top;
        sim1Path.style.width = sim1InitialState.path.width;
        sim1Path.style.transform = sim1InitialState.path.transform;

        sim1Result.classList.remove('opacity-100');
        sim1Result.classList.add('opacity-0', 'absolute');
        sim1Initial.classList.remove('opacity-0', 'absolute');
        sim1Initial.classList.add('opacity-100');
    }

    runSim1Btn.addEventListener('click', runSim1);
    resetSim1Btn.addEventListener('click', resetSim1);
    
    const runSim2Step1Btn = document.getElementById('run-sim2-step1');
    const runSim2Step2Btn = document.getElementById('run-sim2-step2');
    const resetSim2Btn = document.getElementById('reset-sim2');
    
    const sim2VanA = document.getElementById('sim2-vanA');
    const sim2VanB = document.getElementById('sim2-vanB');
    const sim2PathA = document.getElementById('sim2-pathA');
    const sim2PathB = document.getElementById('sim2-pathB');
    
    const sim2InitialPanel = document.getElementById('sim2-initial');
    const sim2Step2Panel = document.getElementById('sim2-step2');
    const sim2ResultPanel = document.getElementById('sim2-result');

    const sim2InitialState = {
        vanA: { left: '20%', top: '20%' },
        vanB: { left: '80%', top: '20%' },
        pathA: { opacity: '0', width: '2px', height: '0', top: '20%', left: '20%', transform: 'translateX(-50%)' }, // Added left and transform for accurate positioning
        pathB: { opacity: '0', width: '2px', height: '0', top: '20%', left: '80%', transform: 'translateX(-50%)' }, // Added left and transform for accurate positioning
    };

    function runSim2Step1() {
        runSim2Step1Btn.disabled = true;
        
        // Reset path A to initial state before starting animation
        sim2PathA.style.opacity = sim2InitialState.pathA.opacity;
        sim2PathA.style.height = sim2InitialState.pathA.height;
        sim2PathA.style.top = sim2InitialState.pathA.top;
        sim2PathA.style.width = sim2InitialState.pathA.width;
        sim2PathA.style.left = sim2InitialState.pathA.left; // Ensure left is reset
        sim2PathA.style.transform = sim2InitialState.pathA.transform;

        // Animate path A drawing
        setTimeout(() => {
            sim2PathA.style.opacity = '1';
            sim2PathA.style.height = '55%'; // From 20% to 75% top is 55% distance
        }, 100); 
        
        // Animate van A movement along the path
        setTimeout(() => {
            sim2VanA.style.left = '30%';
            sim2VanA.style.top = '75%';
        }, 1500); // Start van movement after path is mostly drawn
        
        // Show step 2 panel
        setTimeout(() => {
            sim2InitialPanel.classList.remove('opacity-100');
            sim2InitialPanel.classList.add('opacity-0', 'absolute');
            sim2Step2Panel.classList.remove('opacity-0', 'absolute');
            sim2Step2Panel.classList.add('opacity-100');
        }, 3000); // Adjust timing based on combined animation duration
    }

    function runSim2Step2() {
        runSim2Step2Btn.disabled = true;
        sim2VanA.classList.add('border-red-500', 'border-4'); // Indicate constraint violation on Van A

        setTimeout(() => {
            sim2VanA.classList.remove('border-red-500', 'border-4'); // Remove red border
            
            // Reset path B to initial state before starting animation
            sim2PathB.style.opacity = sim2InitialState.pathB.opacity;
            sim2PathB.style.height = sim2InitialState.pathB.height;
            sim2PathB.style.top = sim2InitialState.pathB.top;
            sim2PathB.style.width = sim2InitialState.pathB.width;
            sim2PathB.style.left = sim2InitialState.pathB.left; // Ensure left is reset
            sim2PathB.style.transform = sim2InitialState.pathB.transform;

            // Animate path B drawing
            setTimeout(() => {
                sim2PathB.style.opacity = '1';
                sim2PathB.style.height = '65%'; // From 20% to 85% top is 65% distance
            }, 100); 

            // Animate van B movement along the path
            setTimeout(() => {
                sim2VanB.style.left = '40%';
                sim2VanB.style.top = '85%';
            }, 1500); // Start van movement after path is mostly drawn

        }, 1500); // Delay before starting Van B's animation

        // Show result panel
        setTimeout(() => {
            sim2Step2Panel.classList.remove('opacity-100');
            sim2Step2Panel.classList.add('opacity-0', 'absolute');
            sim2ResultPanel.classList.remove('opacity-0', 'absolute');
            sim2ResultPanel.classList.add('opacity-100');
        }, 4000); // Adjust timing based on combined animation duration
    }

    function resetSim2() {
        runSim2Step1Btn.disabled = false;
        runSim2Step2Btn.disabled = false;

        sim2VanA.style.left = sim2InitialState.vanA.left;
        sim2VanA.style.top = sim2InitialState.vanA.top;
        sim2VanB.style.left = sim2InitialState.vanB.left;
        sim2VanB.style.top = sim2InitialState.vanB.top;
        
        sim2PathA.style.opacity = sim2InitialState.pathA.opacity;
        sim2PathA.style.width = sim2InitialState.pathA.width;
        sim2PathA.style.height = sim2InitialState.pathA.height;
        sim2PathA.style.top = sim2InitialState.pathA.top;
        sim2PathA.style.left = sim2InitialState.pathA.left;
        sim2PathA.style.transform = sim2InitialState.pathA.transform;

        sim2PathB.style.opacity = sim2InitialState.pathB.opacity;
        sim2PathB.style.width = sim2InitialState.pathB.width;
        sim2PathB.style.height = sim2InitialState.pathB.height;
        sim2PathB.style.top = sim2InitialState.pathB.top;
        sim2PathB.style.left = sim2InitialState.pathB.left;
        sim2PathB.style.transform = sim2InitialState.pathB.transform;
        
        sim2ResultPanel.classList.remove('opacity-100');
        sim2ResultPanel.classList.add('opacity-0', 'absolute');
        sim2Step2Panel.classList.remove('opacity-100');
        sim2Step2Panel.classList.add('opacity-0', 'absolute');
        sim2InitialPanel.classList.remove('opacity-0', 'absolute');
        sim2InitialPanel.classList.add('opacity-100');
    }

    runSim2Step1Btn.addEventListener('click', runSim2Step1);
    runSim2Step2Btn.addEventListener('click', runSim2Step2);
    resetSim2Btn.addEventListener('click', resetSim2);

    updateChartLanguage(); 
});
</script>
</body>
</html>
