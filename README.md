# the-future
Interactive 3D Landing Page for Export, Import &amp; Customs Clearance Course in Faisalabad, Pakistan. Features real-time 3D Three.js trade globe with animated cargo vessel and airplane, interactive 8-week syllabus, ROI salary calculator, and direct WhatsApp registration.
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Export Import & Customs Clearance Course in Faisalabad</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Three.js 3D Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        navy: {
                            900: '#07170d', // Deep Matcha Dark Background
                            800: '#0f2416', // Dark Forest Surface
                            700: '#16331f', // Surface Card
                            600: '#1e442a',
                            500: '#285736',
                        },
                        amber: {
                            accent: '#22c55e', // Vibrant Matcha Emerald Accent
                            bright: '#4ade80', // Glowing Matcha Light
                            light: '#dcfce7',
                        },
                        emerald: {
                            wa: '#1fa855',
                            bright: '#22c55e',
                        }
                    },
                    fontFamily: {
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                        display: ['"Space Grotesk"', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #07170d;
            color: #ffffff;
            overflow-x: hidden;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #07170d;
        }
        ::-webkit-scrollbar-thumb {
            background: #163821;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #22c55e;
        }

        .glass-panel {
            background: rgba(15, 41, 24, 0.88);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(34, 197, 94, 0.3);
        }

        .glass-card {
            background: rgba(22, 56, 33, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .glass-card:hover {
            border-color: rgba(74, 222, 128, 0.6);
            transform: translateY(-4px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.5);
        }

        .glow-amber {
            box-shadow: 0 0 30px rgba(34, 197, 94, 0.35);
        }

        .glow-wa {
            box-shadow: 0 0 25px rgba(31, 168, 85, 0.45);
        }

        .canvas-overlay {
            pointer-events: none;
            background: radial-gradient(circle at center, transparent 35%, rgba(7, 23, 13, 0.88) 100%);
        }
    </style>
</head>
<body class="selection:bg-emerald-bright selection:text-navy-900">

    <!-- FLOATING GLASS NAVIGATION -->
    <nav class="fixed top-0 left-0 w-full z-50 px-4 md:px-8 py-4 transition-all duration-300">
        <div class="max-w-7xl mx-auto glass-panel rounded-2xl px-6 py-3.5 flex items-center justify-between shadow-2xl">
            <!-- Brand & City Tag -->
            <a href="#" class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-emerald-wa to-emerald-bright flex items-center justify-center font-display font-black text-white text-xl shadow-lg">
                    <i class="fa-solid fa-ship"></i>
                </div>
                <div class="flex flex-col">
                    <span class="font-display font-bold text-lg md:text-xl text-white tracking-wide leading-none">EXPORT IMPORT</span>
                    <span class="text-[10px] tracking-[0.25em] text-emerald-bright font-bold uppercase mt-1">Customs Clearance • Faisalabad</span>
                </div>
            </a>

            <!-- Nav Links -->
            <div class="hidden md:flex items-center gap-8 text-sm font-semibold text-white">
                <a href="#why" class="hover:text-amber-bright transition-colors">Why Learn</a>
                <a href="#curriculum" class="hover:text-amber-bright transition-colors">Curriculum</a>
                <a href="#eligibility" class="hover:text-amber-bright transition-colors">Eligibility</a>
                <a href="#fee" class="hover:text-amber-bright transition-colors">Fee & ROI</a>
                <a href="#contact" class="hover:text-amber-bright transition-colors">Contact</a>
            </div>

            <!-- WhatsApp Action -->
            <a href="https://wa.me/923213376758?text=Assalam%20o%20Alaikum%2C%20I%20want%20to%20join%20the%20Export%20Import%20Course" target="_blank" class="bg-emerald-wa hover:bg-emerald-bright text-white font-bold px-5 py-2.5 rounded-xl text-sm transition-all transform hover:scale-105 shadow-lg flex items-center gap-2">
                <i class="fa-brands fa-whatsapp text-lg"></i>
                <span class="hidden sm:inline">WhatsApp Now</span>
            </a>
        </div>
    </nav>

    <!-- 3D GLOBE CANVAS BACKGROUND -->
    <div class="fixed inset-0 z-0 pointer-events-auto" id="canvas-container"></div>
    <div class="fixed inset-0 z-0 canvas-overlay"></div>

    <!-- MAIN CONTENT LAYER -->
    <main class="relative z-10">

        <!-- HERO SECTION -->
        <section class="min-h-screen pt-32 pb-20 flex flex-col justify-between px-6 md:px-12 max-w-7xl mx-auto pointer-events-none">
            <div class="max-w-2xl mt-4 pointer-events-auto">
                <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-emerald-bright/20 border border-emerald-bright/50 text-white text-xs font-bold tracking-wider uppercase mb-6 backdrop-blur-md">
                    <span class="w-2 h-2 rounded-full bg-emerald-bright animate-ping"></span>
                    Admissions Open • Faisalabad Batch 2026
                </div>
                <h1 class="font-display text-4xl sm:text-5xl md:text-6xl font-extrabold tracking-tight leading-[1.15] text-white mb-6">
                    Learn Export, Import & <span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-bright via-green-300 to-amber-light">Customs Clearance</span> in 2 Months
                </h1>
                <p class="text-white text-base md:text-lg leading-relaxed font-normal mb-8">
                    Practical, job-focused training directly from a working Customs Clearance & Export Officer. Master EFS, WeBOC, PSW, GD filing, and complete shipping documentation with live industry examples.
                </p>

                <!-- Hero CTAs -->
                <div class="flex flex-wrap items-center gap-4">
                    <a href="https://wa.me/923213376758?text=Assalam%20o%20Alaikum%2C%20I%20want%20to%20join%20the%20Export%20Import%20Course" target="_blank" class="bg-emerald-wa hover:bg-emerald-bright text-white font-bold px-8 py-4 rounded-xl text-base shadow-xl glow-wa hover:scale-105 transition-all flex items-center gap-3">
                        <i class="fa-brands fa-whatsapp text-2xl"></i>
                        <span>WhatsApp Us Now</span>
                    </a>
                    <a href="#register" class="bg-emerald-bright hover:bg-green-400 text-navy-900 font-extrabold px-8 py-4 rounded-xl text-base shadow-xl glow-amber hover:scale-105 transition-all">
                        Register Seat — Rs 50,000
                    </a>
                </div>
            </div>

            <!-- Key Hero Stats Banner -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mt-16 pointer-events-auto">
                <div class="glass-panel p-5 rounded-2xl">
                    <div class="text-emerald-bright font-display font-bold text-3xl">2 Months</div>
                    <div class="text-white text-xs font-medium mt-1">Complete Practical Course</div>
                </div>
                <div class="glass-panel p-5 rounded-2xl">
                    <div class="text-emerald-bright font-display font-bold text-3xl">Rs 60K+</div>
                    <div class="text-white text-xs font-medium mt-1">Monthly Earning Potential</div>
                </div>
                <div class="glass-panel p-5 rounded-2xl">
                    <div class="text-emerald-bright font-display font-bold text-3xl">Live WeBOC</div>
                    <div class="text-white text-xs font-medium mt-1">Real GD & PSW Filing</div>
                </div>
                <div class="glass-panel p-5 rounded-2xl">
                    <div class="text-emerald-bright font-display font-bold text-3xl">Verified</div>
                    <div class="text-white text-xs font-medium mt-1">Certificate on Completion</div>
                </div>
            </div>

            <!-- Interactive Hint -->
            <div class="text-center pt-8 pointer-events-auto opacity-90 hover:opacity-100 transition-opacity">
                <span class="text-xs font-bold uppercase tracking-widest text-white block mb-2">Drag 3D Globe To Rotate Cargo Routes</span>
                <div class="w-5 h-8 border-2 border-emerald-bright/60 rounded-full mx-auto flex justify-center p-1">
                    <div class="w-1 h-2 bg-emerald-bright rounded-full animate-bounce"></div>
                </div>
            </div>
        </section>

        <!-- WHY LEARN SECTION -->
        <section id="why" class="py-24 px-6 md:px-12 max-w-7xl mx-auto">
            <div class="text-center max-w-2xl mx-auto mb-16">
                <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">High-Demand Skill</span>
                <h2 class="font-display text-3xl sm:text-4xl font-bold text-white mt-2">Why Learn Export Import & Customs?</h2>
                <p class="text-white text-sm md:text-base mt-4 font-normal">Faisalabad is Pakistan's textile and manufacturing hub. Every factory, trader, and freight forwarder needs trained documentation officers.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <div class="glass-card p-6 rounded-2xl">
                    <div class="w-12 h-12 rounded-xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mb-5">
                        <i class="fa-solid fa-briefcase"></i>
                    </div>
                    <h3 class="font-display font-bold text-xl text-white mb-2">Job Security</h3>
                    <p class="text-xs text-white leading-relaxed font-normal">International trade never stops. Exporters, importers, clearing agencies, and shipping lines always require skilled personnel.</p>
                </div>

                <div class="glass-card p-6 rounded-2xl">
                    <div class="w-12 h-12 rounded-xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mb-5">
                        <i class="fa-solid fa-money-bill-trend-up"></i>
                    </div>
                    <h3 class="font-display font-bold text-xl text-white mb-2">Rs 60,000+ Earning</h3>
                    <p class="text-xs text-white leading-relaxed font-normal">Skilled documentation and clearance officers command lucrative salaries depending on skill, company size, and expertise.</p>
                </div>

                <div class="glass-card p-6 rounded-2xl">
                    <div class="w-12 h-12 rounded-xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mb-5">
                        <i class="fa-solid fa-globe"></i>
                    </div>
                    <h3 class="font-display font-bold text-xl text-white mb-2">Career Versatility</h3>
                    <p class="text-xs text-white leading-relaxed font-normal">Work in textile mills, freight forwarding firms, shipping lines, clearing agencies, or launch your own international trading business.</p>
                </div>

                <div class="glass-card p-6 rounded-2xl">
                    <div class="w-12 h-12 rounded-xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mb-5">
                        <i class="fa-solid fa-laptop-code"></i>
                    </div>
                    <h3 class="font-display font-bold text-xl text-white mb-2">Hands-On Practical</h3>
                    <p class="text-xs text-white leading-relaxed font-normal">Learn on real GD filings, WeBOC/PSW live portal demos, and mock export/import shipments, not just dry textbook theory.</p>
                </div>
            </div>
        </section>

        <!-- CURRICULUM ACCORDION SECTION -->
        <section id="curriculum" class="py-24 px-6 md:px-12 max-w-5xl mx-auto">
            <div class="text-center max-w-2xl mx-auto mb-16">
                <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">8-Week Detailed Syllabus</span>
                <h2 class="font-display text-3xl sm:text-4xl font-bold text-white mt-2">What You Will Learn</h2>
                <p class="text-white text-sm md:text-base mt-4 font-normal">Step-by-step roadmap from absolute basics to advanced live shipment filing.</p>
            </div>

            <div class="space-y-4">
                <!-- Module 1 -->
                <div class="glass-panel rounded-2xl overflow-hidden border border-white/20">
                    <button onclick="toggleAccordion('acc-1')" class="w-full p-6 text-left flex items-center justify-between font-display font-bold text-lg text-white hover:text-amber-bright transition-colors">
                        <div class="flex items-center gap-4">
                            <span class="w-10 h-10 rounded-xl bg-amber-accent/30 text-amber-bright font-extrabold flex items-center justify-center text-sm">W 1-2</span>
                            <span>Weeks 1–2: Foundation & Export Documents</span>
                        </div>
                        <i id="icon-acc-1" class="fa-solid fa-chevron-down text-amber-bright transition-transform"></i>
                    </button>
                    <div id="acc-1" class="hidden px-6 pb-6 text-sm text-white space-y-3 border-t border-white/10 pt-4 font-normal">
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Export/Import basics, Incoterms 2020 rules, HS / PCT Codes classification</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>NTN, STRN, WeBOC and Pakistan Single Window (PSW) registration process</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Drafting Commercial Invoice, Packing List, Bill of Lading (B/L), Airway Bill (AWB)</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Certificate of Origin (Chamber of Commerce), Phytosanitary & Health Certificates</span></div>
                    </div>
                </div>

                <!-- Module 2 -->
                <div class="glass-panel rounded-2xl overflow-hidden border border-white/20">
                    <button onclick="toggleAccordion('acc-2')" class="w-full p-6 text-left flex items-center justify-between font-display font-bold text-lg text-white hover:text-amber-bright transition-colors">
                        <div class="flex items-center gap-4">
                            <span class="w-10 h-10 rounded-xl bg-amber-accent/30 text-amber-bright font-extrabold flex items-center justify-center text-sm">W 3-4</span>
                            <span>Weeks 3–4: Export Procedure & EFS Scheme</span>
                        </div>
                        <i id="icon-acc-2" class="fa-solid fa-chevron-down text-amber-bright transition-transform"></i>
                    </button>
                    <div id="acc-2" class="hidden px-6 pb-6 text-sm text-white space-y-3 border-t border-white/10 pt-4 font-normal">
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Step-by-step Export Goods Declaration (GD) filing on WeBOC system</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Bank E-Form generation and tracking export proceeds realization</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Export Facilitation Scheme (EFS), DTRE, Duty Drawback, and Sales Tax Refund mechanisms</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Port procedures, container stuffing, LEO (Let Export Order), and shipping line release</span></div>
                    </div>
                </div>

                <!-- Module 3 -->
                <div class="glass-panel rounded-2xl overflow-hidden border border-white/20">
                    <button onclick="toggleAccordion('acc-3')" class="w-full p-6 text-left flex items-center justify-between font-display font-bold text-lg text-white hover:text-amber-bright transition-colors">
                        <div class="flex items-center gap-4">
                            <span class="w-10 h-10 rounded-xl bg-amber-accent/30 text-amber-bright font-extrabold flex items-center justify-center text-sm">W 5-6</span>
                            <span>Weeks 5–6: Import & Customs Clearance</span>
                        </div>
                        <i id="icon-acc-3" class="fa-solid fa-chevron-down text-amber-bright transition-transform"></i>
                    </button>
                    <div id="acc-3" class="hidden px-6 pb-6 text-sm text-white space-y-3 border-t border-white/10 pt-4 font-normal">
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Import documents, Letter of Credit (LC), Telegraphic Transfer (TT), and payment terms</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Import GD filing, IGM (Import General Manifest), and Delivery Order (DO) issuance</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Customs valuation, Customs Duty, Sales Tax, Income Tax & Additional Duty calculations</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Assessment, physical examination, port demurrage, and container detention handling</span></div>
                    </div>
                </div>

                <!-- Module 4 -->
                <div class="glass-panel rounded-2xl overflow-hidden border border-white/20">
                    <button onclick="toggleAccordion('acc-4')" class="w-full p-6 text-left flex items-center justify-between font-display font-bold text-lg text-white hover:text-amber-bright transition-colors">
                        <div class="flex items-center gap-4">
                            <span class="w-10 h-10 rounded-xl bg-amber-accent/30 text-amber-bright font-extrabold flex items-center justify-center text-sm">W 7-8</span>
                            <span>Weeks 7–8: Advanced Topics & Live Mock Shipments</span>
                        </div>
                        <i id="icon-acc-4" class="fa-solid fa-chevron-down text-amber-bright transition-transform"></i>
                    </button>
                    <div id="acc-4" class="hidden px-6 pb-6 text-sm text-white space-y-3 border-t border-white/10 pt-4 font-normal">
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>SROs notifications, Free Trade Agreements (FTAs), GSP+, Transit Trade, Courier shipments</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Resolving Classification (HS Code) and Customs Valuation disputes</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Complete end-to-end mock export and import shipment from start to finish</span></div>
                        <div class="flex items-start gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base mt-0.5"></i><span>Final practical assessment test and Course Completion Certificate award</span></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ELIGIBILITY & SALARY VISUALIZER SECTION -->
        <section id="eligibility" class="py-24 px-6 md:px-12 max-w-7xl mx-auto">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                
                <!-- Who Can Join -->
                <div class="glass-panel p-8 rounded-3xl border border-white/20">
                    <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">No Prior Experience Needed</span>
                    <h2 class="font-display text-3xl font-bold text-white mt-2 mb-6">Who Can Join This Course?</h2>
                    
                    <ul class="space-y-4 text-sm text-white font-medium">
                        <li class="flex items-center gap-3 bg-navy-800/90 p-4 rounded-xl border border-white/10">
                            <i class="fa-solid fa-circle-check text-emerald-bright text-lg"></i>
                            <span class="text-white">Intermediate (FA / FSc / ICom) graduates</span>
                        </li>
                        <li class="flex items-center gap-3 bg-navy-800/90 p-4 rounded-xl border border-white/10">
                            <i class="fa-solid fa-circle-check text-emerald-bright text-lg"></i>
                            <span class="text-white">Graduates (BA / BCom / BBA / BS or equivalent)</span>
                        </li>
                        <li class="flex items-center gap-3 bg-navy-800/90 p-4 rounded-xl border border-white/10">
                            <i class="fa-solid fa-circle-check text-emerald-bright text-lg"></i>
                            <span class="text-white">Job seekers & fresh university graduates</span>
                        </li>
                        <li class="flex items-center gap-3 bg-navy-800/90 p-4 rounded-xl border border-white/10">
                            <i class="fa-solid fa-circle-check text-emerald-bright text-lg"></i>
                            <span class="text-white">Traders & factory owners planning to export or import</span>
                        </li>
                        <li class="flex items-center gap-3 bg-navy-800/90 p-4 rounded-xl border border-white/10">
                            <i class="fa-solid fa-circle-check text-emerald-bright text-lg"></i>
                            <span class="text-white">Existing staff working in accounts, logistics, or clearance</span>
                        </li>
                    </ul>
                </div>

                <!-- Interactive Salary & Career Calculator -->
                <div class="glass-panel p-8 rounded-3xl border border-amber-accent/30 relative">
                    <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">Career Earning Estimator</span>
                    <h3 class="font-display text-2xl font-bold text-white mt-1 mb-4">Salary Growth Potential</h3>
                    
                    <div class="space-y-6">
                        <div>
                            <div class="flex justify-between text-xs font-bold mb-2">
                                <span class="text-white">Fresh Documentation Junior</span>
                                <span class="text-amber-bright">Rs 35,000 - 45,000 / mo</span>
                            </div>
                            <div class="w-full h-3 bg-navy-900 rounded-full overflow-hidden p-0.5 border border-navy-500">
                                <div class="h-full bg-gradient-to-r from-amber-accent to-amber-bright rounded-full" style="width: 40%;"></div>
                            </div>
                        </div>

                        <div>
                            <div class="flex justify-between text-xs font-bold mb-2">
                                <span class="text-white">Export / Clearance Officer (1-2 Yrs)</span>
                                <span class="text-amber-bright">Rs 60,000 - 90,000 / mo</span>
                            </div>
                            <div class="w-full h-3 bg-navy-900 rounded-full overflow-hidden p-0.5 border border-navy-500">
                                <div class="h-full bg-gradient-to-r from-amber-accent to-amber-bright rounded-full" style="width: 70%;"></div>
                            </div>
                        </div>

                        <div>
                            <div class="flex justify-between text-xs font-bold mb-2">
                                <span class="text-white">Senior Export Manager / Independent Broker</span>
                                <span class="text-amber-bright">Rs 120,000+ / mo</span>
                            </div>
                            <div class="w-full h-3 bg-navy-900 rounded-full overflow-hidden p-0.5 border border-navy-500">
                                <div class="h-full bg-gradient-to-r from-amber-accent to-amber-bright rounded-full" style="width: 95%;"></div>
                            </div>
                        </div>
                    </div>

                    <div class="mt-6 pt-4 border-t border-white/10 text-xs text-white/90 font-normal">
                        *Note: Salary figures are estimates based on Faisalabad industry standards and individual skills.
                    </div>
                </div>

            </div>
        </section>

        <!-- FEE & ROI SECTION -->
        <section id="fee" class="py-24 px-6 md:px-12 max-w-4xl mx-auto">
            <div class="glass-panel p-8 md:p-12 rounded-3xl border-2 border-amber-accent text-center relative overflow-hidden glow-amber">
                <div class="absolute -top-10 -right-10 w-40 h-40 bg-amber-accent/10 rounded-full blur-2xl"></div>
                
                <span class="bg-amber-accent/30 text-white text-xs font-extrabold px-4 py-1.5 rounded-full border border-amber-accent/50 uppercase tracking-widest">Single Investment</span>
                <h2 class="font-display text-3xl sm:text-4xl font-bold text-white mt-4">Total Course Fee</h2>
                
                <div class="font-display text-5xl sm:text-6xl font-black text-amber-bright my-6">
                    Rs 50,000
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-xl mx-auto text-left text-sm text-white font-medium mb-8">
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> Full 2 months (8 weeks) training</div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> Live WeBOC / PSW demo access</div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> Document templates & checklists</div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> End-to-end mock shipment practice</div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> Completion Certificate</div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-circle-check text-emerald-bright text-base"></i> Direct instructor guidance</div>
                </div>

                <a href="https://wa.me/923213376758?text=Assalam%20o%20Alaikum%2C%20I%20want%20to%20reserve%20a%20seat%20in%20the%20Export%20Import%20Course" target="_blank" class="bg-amber-accent hover:bg-amber-bright text-navy-900 font-extrabold px-10 py-4 rounded-xl text-lg inline-block transition-all transform hover:scale-105 shadow-xl">
                    Reserve My Seat Now
                </a>
            </div>
        </section>

        <!-- REGISTRATION FORM SECTION -->
        <section id="register" class="py-24 px-6 md:px-12 max-w-3xl mx-auto">
            <div class="glass-panel p-8 md:p-10 rounded-3xl border border-white/20">
                <div class="text-center mb-8">
                    <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">Instant Admission Form</span>
                    <h2 class="font-display text-3xl font-bold text-white mt-1">Register for the Next Batch</h2>
                    <p class="text-white text-xs md:text-sm mt-2 font-normal">Fill in your details below to continue registration directly on WhatsApp.</p>
                </div>

                <form id="reg-form" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-white mb-1.5">Full Name</label>
                        <input type="text" id="form-name" placeholder="e.g. Muhammad Ali" required class="w-full px-4 py-3 rounded-xl bg-navy-800 border border-white/20 text-white placeholder-white/50 focus:outline-none focus:border-amber-accent transition-colors font-medium">
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-white mb-1.5">Phone / WhatsApp Number</label>
                        <input type="tel" id="form-phone" placeholder="e.g. 0300 1234567" required class="w-full px-4 py-3 rounded-xl bg-navy-800 border border-white/20 text-white placeholder-white/50 focus:outline-none focus:border-amber-accent transition-colors font-medium">
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-white mb-1.5">Highest Qualification</label>
                        <select id="form-qual" class="w-full px-4 py-3 rounded-xl bg-navy-800 border border-white/20 text-white focus:outline-none focus:border-amber-accent transition-colors font-medium">
                            <option value="Intermediate">Intermediate (FA / FSc / ICom)</option>
                            <option value="Graduation">Graduation (BA / BCom / BBA / BS)</option>
                            <option value="Master/Other">Master / Other Professional</option>
                        </select>
                    </div>

                    <button type="submit" class="w-full bg-emerald-wa hover:bg-emerald-bright text-white font-bold py-4 rounded-xl text-base transition-all flex items-center justify-center gap-2 shadow-lg glow-wa">
                        <i class="fa-brands fa-whatsapp text-xl"></i>
                        <span>Send Registration Details on WhatsApp</span>
                    </button>
                </form>
            </div>
        </section>

        <!-- CONTACT & LOCATION SECTION -->
        <section id="contact" class="py-24 px-6 md:px-12 max-w-7xl mx-auto">
            <div class="text-center max-w-2xl mx-auto mb-16">
                <span class="text-amber-bright font-bold tracking-widest uppercase text-xs">Training Academy</span>
                <h2 class="font-display text-3xl font-bold text-white mt-1">Contact & Campus Details</h2>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- WhatsApp -->
                <a href="https://wa.me/923213376758" target="_blank" class="glass-card p-6 rounded-2xl text-center group">
                    <div class="w-14 h-14 rounded-2xl bg-emerald-wa/30 text-white text-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform">
                        <i class="fa-brands fa-whatsapp"></i>
                    </div>
                    <h3 class="font-display font-bold text-lg text-white">WhatsApp & Call</h3>
                    <p class="text-amber-bright font-bold text-sm mt-1">+92 321 3376758</p>
                </a>

                <!-- Email -->
                <a href="mailto:hamzanouman231@gmail.com" class="glass-card p-6 rounded-2xl text-center group">
                    <div class="w-14 h-14 rounded-2xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-envelope"></i>
                    </div>
                    <h3 class="font-display font-bold text-lg text-white">Email Address</h3>
                    <p class="text-white font-medium text-sm mt-1">hamzanouman231@gmail.com</p>
                </a>

                <!-- Location -->
                <div class="glass-card p-6 rounded-2xl text-center">
                    <div class="w-14 h-14 rounded-2xl bg-amber-accent/30 text-amber-bright text-2xl flex items-center justify-center mx-auto mb-4">
                        <i class="fa-solid fa-location-dot"></i>
                    </div>
                    <h3 class="font-display font-bold text-lg text-white">Campus Location</h3>
                    <p class="text-white font-medium text-sm mt-1">BC Tower, Jinnah Colony, Faisalabad, Pakistan</p>
                </div>
            </div>
        </section>

        <!-- FOOTER -->
        <footer class="border-t border-navy-500/50 bg-navy-900 py-8 px-6 text-center text-xs text-white">
            <div class="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4 font-medium">
                <div>© 2026 Export Import & Customs Clearance Training • Faisalabad</div>
                <div>Designed for Practical Career Growth</div>
            </div>
        </footer>

    </main>

    <!-- FLOATING WHATSAPP BUTTON -->
    <a href="https://wa.me/923213376758?text=Assalam%20o%20Alaikum%2C%20I%20want%20details%20about%20the%20Export%20Import%20Course" target="_blank" class="fixed bottom-6 right-6 z-50 bg-emerald-wa hover:bg-emerald-bright text-white font-bold px-5 py-3.5 rounded-full shadow-2xl flex items-center gap-2 glow-wa hover:scale-110 transition-all text-sm">
        <i class="fa-brands fa-whatsapp text-2xl"></i>
        <span>Chat on WhatsApp</span>
    </a>

    <!-- THREE.JS 3D TRADE GLOBE SCRIPT -->
    <script>
        let scene, camera, renderer, globeGroup, containerGroup;
        let isDragging = false;
        let previousMousePosition = { x: 0, y: 0 };

        function init3D() {
            const container = document.getElementById('canvas-container');

            // 1. Scene
            scene = new THREE.Scene();
            scene.fog = new THREE.FogExp2(0x0a1020, 0.08);

            // 2. Camera
            camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.z = 8.5;

            // 3. Renderer
            renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            container.appendChild(renderer.domElement);

            // 4. Lights
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.85);
            scene.add(ambientLight);

            const pointLight = new THREE.PointLight(0x22c55e, 3.0, 20);
            pointLight.position.set(5, 5, 5);
            scene.add(pointLight);

            // 5. Globe Group
            globeGroup = new THREE.Group();

            // Inner Globe Sphere (Matcha dark green tint)
            const sphereGeo = new THREE.SphereGeometry(2.2, 32, 32);
            const sphereMat = new THREE.MeshBasicMaterial({ color: 0x0f2416, transparent: true, opacity: 0.9 });
            const innerSphere = new THREE.Mesh(sphereGeo, sphereMat);
            globeGroup.add(innerSphere);

            // Outer Wireframe Wire (Matcha green wireframe)
            const wireGeo = new THREE.SphereGeometry(2.22, 24, 16);
            const wireMat = new THREE.MeshBasicMaterial({ color: 0x22c55e, wireframe: true, transparent: true, opacity: 0.45 });
            const wireSphere = new THREE.Mesh(wireGeo, wireMat);
            globeGroup.add(wireSphere);

            // Orbiting Cargo Containers (Green palettes)
            containerGroup = new THREE.Group();
            const colors = [0x22c55e, 0x1fa855, 0x4ade80, 0x86efac, 0xfbbf24];

            for (let i = 0; i < 20; i++) {
                const boxGeo = new THREE.BoxGeometry(0.5, 0.25, 0.25);
                const boxMat = new THREE.MeshBasicMaterial({ color: colors[i % colors.length] });
                const box = new THREE.Mesh(boxGeo, boxMat);

                const pivot = new THREE.Object3D();
                pivot.rotation.set(Math.random() * Math.PI * 2, Math.random() * Math.PI * 2, 0);
                box.position.x = 3.1 + (i % 3) * 0.3;

                pivot.add(box);
                pivot.userData = { speed: 0.003 + Math.random() * 0.005 };
                containerGroup.add(pivot);
            }

            globeGroup.add(containerGroup);

            // Set Position (right side on desktop)
            globeGroup.position.x = window.innerWidth > 800 ? 2.5 : 0;
            scene.add(globeGroup);

            // Resize & Controls
            window.addEventListener('resize', onWindowResize);

            window.addEventListener('mousedown', (e) => {
                isDragging = true;
                previousMousePosition = { x: e.clientX, y: e.clientY };
            });

            window.addEventListener('mousemove', (e) => {
                if (!isDragging) return;
                const deltaX = e.clientX - previousMousePosition.x;
                const deltaY = e.clientY - previousMousePosition.y;

                globeGroup.rotation.y += deltaX * 0.005;
                globeGroup.rotation.x += deltaY * 0.005;

                previousMousePosition = { x: e.clientX, y: e.clientY };
            });

            window.addEventListener('mouseup', () => { isDragging = false; });

            animate();
        }

        function animate() {
            requestAnimationFrame(animate);

            if (globeGroup) {
                globeGroup.rotation.y += 0.003;
            }

            if (containerGroup) {
                containerGroup.children.forEach(pivot => {
                    pivot.rotation.y += pivot.userData.speed;
                });
            }

            renderer.render(scene, camera);
        }

        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
            if (globeGroup) {
                globeGroup.position.x = window.innerWidth > 800 ? 2.5 : 0;
            }
        }

        // Accordion Toggle Function
        function toggleAccordion(id) {
            const content = document.getElementById(id);
            const icon = document.getElementById(`icon-${id}`);

            if (content.classList.contains('hidden')) {
                content.classList.remove('hidden');
                icon.classList.add('rotate-180');
            } else {
                content.classList.add('hidden');
                icon.classList.remove('rotate-180');
            }
        }

        // WhatsApp Form Handler
        document.getElementById('reg-form').addEventListener('submit', function (e) {
            e.preventDefault();
            const name = document.getElementById('form-name').value;
            const phone = document.getElementById('form-phone').value;
            const qual = document.getElementById('form-qual').value;

            const msg = `Assalam o Alaikum, I want to join the Export Import Course in Faisalabad.\nName: ${name}\nPhone: ${phone}\nQualification: ${qual}`;
            window.open(`https://wa.me/923213376758?text=${encodeURIComponent(msg)}`, '_blank');
        });

        // Initialize 3D Scene
        window.onload = function() {
            init3D();
        };
    </script>
</body>
</html>
