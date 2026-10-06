import React, { useState, useEffect } from 'react';

export default function App() {
  // Navigation & UI state
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [activeTab, setActiveTab] = useState('all');
  const [scrolled, setScrolled] = useState(false);
  
  // Reservation form state
  const [reservation, setReservation] = useState({
    name: '',
    email: '',
    phone: '',
    date: '',
    time: '18:00',
    guests: '2',
    seating: 'indoor',
    notes: ''
  });
  const [resSubmitted, setResSubmitted] = useState(false);

  // Handle scroll for sticky header shadow
  useEffect(() => {
    const handleScroll = () => {
      if (window.scrollY > 40) {
        setScrolled(true);
      } else {
        setScrolled(false);
      }
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setReservation(prev => ({ ...prev, [name]: value }));
  };

  const handleReservationSubmit = (e) => {
    e.preventDefault();
    if (!reservation.name || !reservation.email || !reservation.date || !reservation.phone) {
      alert('Please fill out all required fields.');
      return;
    }
    setResSubmitted(true);
  };

  // Menu items data
  const menuItems = [
    {
      id: 1,
      name: "Ethiopian Yirgacheffe Pour-Over",
      category: "coffee",
      price: "$6.50",
      description: "Single-origin beans with delicate floral notes, jasmine aroma, and bright bergamot finish.",
      badge: "Single Origin",
      image: "https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 2,
      name: "Velvet Truffle Mocha",
      category: "coffee",
      price: "$7.00",
      description: "House-crafted dark chocolate ganache blended with double-shot espresso and steamed oat milk.",
      badge: "Signature",
      image: "https://images.unsplash.com/photo-1534778101976-62847782c213?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 3,
      name: "Matcha Ceremonial Latte",
      category: "beverages",
      price: "$7.50",
      description: "First-harvest stone-ground Uji matcha whisked to perfection with vanilla bean infused milk.",
      badge: "Organic",
      image: "https://images.unsplash.com/photo-1536256263959-770b48d82b0a?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 4,
      name: "Truffle Mushroom Sourdough Toast",
      category: "brunch",
      price: "$16.00",
      description: "Wild forest mushrooms sautéed in garlic-herb butter, truffle paste, whipped ricotta on charred sourdough.",
      badge: "Chef's Choice",
      image: "https://images.unsplash.com/photo-1525351484163-7529414344d8?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 5,
      name: "Avocado Burrata Sunshine Bowl",
      category: "brunch",
      price: "$18.50",
      description: "Fresh burrata cheese, smashed heirloom avocado, poached farm eggs, dukkah spice, micro-greens.",
      badge: "Popular",
      image: "https://images.unsplash.com/photo-1540420773420-3366772f4999?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 6,
      name: "Saffron Honey Croissant French Toast",
      category: "brunch",
      price: "$15.00",
      description: "Twice-baked butter croissant soaked in cardamom custard, saffron-infused raw honey, seasonal berries.",
      badge: "Sweet",
      image: "https://images.unsplash.com/photo-1484723091739-30a097e8f929?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 7,
      name: "Pan-Seared Salmon Grain Bowl",
      category: "lunch",
      price: "$22.00",
      description: "Norwegian sustainable salmon, ancient grains, roasted squash, pickled shallots, creamy miso-tahini dressing.",
      badge: "Healthy",
      image: "https://images.unsplash.com/photo-1467003909585-2f8a72700288?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 8,
      name: "Aakay Artisan Wagyu Burger",
      category: "lunch",
      price: "$24.00",
      description: "Grade-A Wagyu beef patty, aged white cheddar, caramelized onion jam, black garlic aioli in a brioche bun.",
      badge: "New",
      image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&q=80&w=600"
    },
    {
      id: 9,
      name: "Cardamom Pistachio Opera Cake",
      category: "desserts",
      price: "$11.00",
      description: "Layers of almond sponge, pistachio buttercream, dark chocolate ganache, infused with aromatic cardamom.",
      badge: "Artisanal",
      image: "https://images.unsplash.com/photo-1578985545062-69928b1d9587?auto=format&fit=crop&q=80&w=600"
    }
  ];

  const filteredMenu = activeTab === 'all' 
    ? menuItems 
    : menuItems.filter(item => item.category === activeTab);

  const galleryImages = [
    "https://images.unsplash.com/photo-1554118811-1e0d58224f24?auto=format&fit=crop&q=80&w=600",
    "https://images.unsplash.com/photo-1442512595331-e89e73853f31?auto=format&fit=crop&q=80&w=600",
    "https://images.unsplash.com/photo-1501339847302-ac426a4a7cbb?auto=format&fit=crop&q=80&w=600",
    "https://images.unsplash.com/photo-1559925393-8be0ec4767c8?auto=format&fit=crop&q=80&w=600",
    "https://images.unsplash.com/photo-1521017432531-fbd92d768814?auto=format&fit=crop&q=80&w=600",
    "https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&q=80&w=600"
  ];

  return (
    <div className="min-h-screen bg-[#fdf9f1] text-[#1c1c17] font-['Plus_Jakarta_Sans',sans-serif] selection:bg-[#fed488] selection:text-[#785a1a]">
      
      {/* HEADER / NAVIGATION */}
      <header className={`fixed top-0 left-0 right-0 z-50 transition-all duration-300 ${scrolled ? 'bg-[#fdf9f1]/90 backdrop-blur-md shadow-sm py-4' : 'bg-transparent py-6'}`}>
        <div className="max-w-7xl mx-auto px-6 md:px-12 flex items-center justify-between">
          <a href="#" className="flex items-center gap-2 group">
            <span className="font-['Playfair_Display'] text-2xl md:text-3xl font-bold tracking-wider text-[#1c1c17] group-hover:text-[#b47b2c] transition-colors">
              AAKAY
            </span>
            <span className="text-xs font-medium tracking-[0.2em] text-[#8c7853] uppercase border-l border-[#8c7853]/40 pl-2 hidden sm:inline">
              Café & Kitchen
            </span>
          </a>

          {/* Desktop Nav Links */}
          <nav className="hidden md:flex items-center gap-8 text-sm font-medium tracking-wide">
            <a href="#about" className="hover:text-[#b47b2c] transition-colors">Our Story</a>
            <a href="#menu" className="hover:text-[#b47b2c] transition-colors">Menu</a>
            <a href="#gallery" className="hover:text-[#b47b2c] transition-colors">Atmosphere</a>
            <a href="#reviews" className="hover:text-[#b47b2c] transition-colors">Reviews</a>
            <a href="#contact" className="hover:text-[#b47b2c] transition-colors">Visit Us</a>
          </nav>

          {/* Action Button */}
          <div className="hidden md:flex items-center gap-4">
            <a 
              href="#reservations" 
              className="bg-[#1c1c17] text-[#fdf9f1] px-6 py-2.5 rounded-full text-xs font-semibold uppercase tracking-wider hover:bg-[#b47b2c] transition-all duration-300 shadow-sm"
            >
              Book a Table
            </a>
          </div>

          {/* Mobile Menu Button */}
          <button 
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
            className="md:hidden text-[#1c1c17] p-2 focus:outline-none"
            aria-label="Toggle Menu"
          >
            <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              {mobileMenuOpen ? (
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M6 18L18 6M6 6l12 12" />
              ) : (
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M4 8h16M4 16h16" />
              )}
            </svg>
          </button>
        </div>

        {/* Mobile Menu Dropdown */}
        {mobileMenuOpen && (
          <div className="absolute top-full left-0 right-0 bg-[#fdf9f1] border-b border-[#e6dcce] py-6 px-8 shadow-lg md:hidden flex flex-col gap-4 text-center">
            <a href="#about" onClick={() => setMobileMenuOpen(false)} className="text-base font-medium py-1">Our Story</a>
            <a href="#menu" onClick={() => setMobileMenuOpen(false)} className="text-base font-medium py-1">Menu</a>
            <a href="#gallery" onClick={() => setMobileMenuOpen(false)} className="text-base font-medium py-1">Atmosphere</a>
            <a href="#reviews" onClick={() => setMobileMenuOpen(false)} className="text-base font-medium py-1">Reviews</a>
            <a href="#contact" onClick={() => setMobileMenuOpen(false)} className="text-base font-medium py-1">Visit Us</a>
            <a 
              href="#reservations" 
              onClick={() => setMobileMenuOpen(false)} 
              className="bg-[#1c1c17] text-[#fdf9f1] py-3 rounded-full text-xs font-semibold uppercase tracking-wider mt-2"
            >
              Book a Table
            </a>
          </div>
        )}
      </header>

      {/* HERO SECTION */}
      <section className="relative pt-32 pb-20 md:pt-44 md:pb-32 overflow-hidden">
        <div className="max-w-7xl mx-auto px-6 md:px-12 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
          
          <div className="lg:col-span-7 flex flex-col items-start gap-6">
            <div className="inline-flex items-center gap-2 bg-[#f0e6d6] px-3.5 py-1.5 rounded-full text-xs font-semibold uppercase tracking-widest text-[#785a1a]">
              <span className="w-2 h-2 rounded-full bg-[#b47b2c]"></span>
              Sanctuary of Taste & Hospitality
            </div>
            
            <h1 className="font-['Playfair_Display'] text-4xl sm:text-6xl lg:text-7xl font-bold tracking-tight text-[#1c1c17] leading-[1.1]">
              Good Food. <br />
              <span className="italic font-normal text-[#b47b2c]">Great Moments.</span>
            </h1>
            
            <p className="text-base md:text-lg text-[#5c564a] max-w-xl leading-relaxed">
              Immerse your senses in handcrafted single-origin coffees, artisanal farm-to-table dining, and a serene, sun-drenched sanctuary designed for soulful conversations.
            </p>
            
            <div className="flex flex-wrap items-center gap-4 pt-2">
              <a 
                href="#menu" 
                className="bg-[#1c1c17] text-[#fdf9f1] px-8 py-4 rounded-full text-xs font-semibold uppercase tracking-wider hover:bg-[#b47b2c] transition-all duration-300 shadow-md"
              >
                Explore Menu
              </a>
              <a 
                href="#reservations" 
                className="border border-[#1c1c17]/30 px-8 py-4 rounded-full text-xs font-semibold uppercase tracking-wider hover:border-[#1c1c17] transition-all duration-300"
              >
                Book a Table
              </a>
            </div>

            <div className="grid grid-cols-3 gap-6 pt-8 border-t border-[#e6dcce] w-full mt-4">
              <div>
                <p className="font-['Playfair_Display'] text-2xl font-bold text-[#1c1c17]">100%</p>
                <p className="text-xs text-[#7c7263] uppercase tracking-wider mt-1">Single-Origin Coffee</p>
              </div>
              <div>
                <p className="font-['Playfair_Display'] text-2xl font-bold text-[#1c1c17]">4.9★</p>
                <p className="text-xs text-[#7c7263] uppercase tracking-wider mt-1">Guest Satisfaction</p>
              </div>
              <div>
                <p className="font-['Playfair_Display'] text-2xl font-bold text-[#1c1c17]">Artisanal</p>
                <p className="text-xs text-[#7c7263] uppercase tracking-wider mt-1">Daily Baked Pastries</p>
              </div>
            </div>
          </div>

          <div className="lg:col-span-5 relative">
            <div className="relative mx-auto max-w-md lg:max-w-none">
              <div className="absolute -inset-4 bg-[#eedecc] rounded-3xl transform rotate-3 -z-10"></div>
              <img 
                src="https://images.unsplash.com/photo-1501339847302-ac426a4a7cbb?auto=format&fit=crop&q=80&w=800" 
                alt="Aakay Cafe Ambiance" 
                className="rounded-2xl shadow-xl object-cover w-full h-[480px] md:h-[540px]"
              />
              <div className="absolute bottom-6 left-6 right-6 bg-[#fdf9f1]/90 backdrop-blur-md p-4 rounded-xl border border-[#e6dcce] shadow-md flex items-center gap-4">
                <div className="w-10 h-10 rounded-full bg-[#b47b2c]/20 flex items-center justify-center text-[#b47b2c] font-bold">☕</div>
                <div>
                  <p className="text-xs font-bold uppercase tracking-wide text-[#1c1c17]">Featured Roast of the Week</p>
                  <p className="text-xs text-[#5c564a]">Ethiopian Yirgacheffe with Jasmine & Bergamot notes</p>
                </div>
              </div>
            </div>
          </div>

        </div>
      </section>

      {/* ABOUT STORY */}
      <section id="about" className="py-24 bg-[#f4ecdf]">
        <div className="max-w-7xl mx-auto px-6 md:px-12 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
          
          <div className="lg:col-span-5 grid grid-cols-2 gap-4">
            <img 
              src="https://images.unsplash.com/photo-1442512595331-e89e73853f31?auto=format&fit=crop&q=80&w=500" 
              alt="Coffee preparation" 
              className="rounded-2xl object-cover w-full h-64 shadow-md"
            />
            <img 
              src="https://images.unsplash.com/photo-1559925393-8be0ec4767c8?auto=format&fit=crop&q=80&w=500" 
              alt="Cafe interior" 
              className="rounded-2xl object-cover w-full h-64 shadow-md mt-8"
            />
          </div>

          <div className="lg:col-span-7 flex flex-col items-start gap-6 lg:pl-8">
            <span className="text-xs font-semibold uppercase tracking-[0.2em] text-[#b47b2c]">Our Philosophy</span>
            <h2 className="font-['Playfair_Display'] text-3xl md:text-5xl font-bold text-[#1c1c17] leading-tight">
              Where exceptional craft meets quiet moments of connection.
            </h2>
            <p className="text-[#5c564a] text-base leading-relaxed">
              Founded with a passion for unhurried hospitality, AAKAY was born out of a simple desire: to create a space where time slows down. Every cup of coffee we pour and every dish we plate is crafted with intention, sourcing only from sustainable farmers and ethical growers who share our deep respect for nature.
            </p>
            <p className="text-[#5c564a] text-base leading-relaxed">
              Whether you are looking for a secluded corner to read your morning journal, holding a quiet meeting over brunch, or celebrating an afternoon with close friends, our doors are open to welcome you home.
            </p>

            <div className="pt-4 flex items-center gap-6">
              <div>
                <p className="font-['Playfair_Display'] text-xl font-bold text-[#1c1c17]">Aarav & Kayra</p>
                <p className="text-xs text-[#7c7263] uppercase tracking-wider">Founders & Culinary Directors</p>
              </div>
              <div className="h-10 w-px bg-[#d8ccc0]"></div>
              <div>
                <span className="font-['Playfair_Display'] italic text-2xl text-[#b47b2c]">"Crafted with love."</span>
              </div>
            </div>
          </div>

        </div>
      </section>

      {/* MENU SECTION */}
      <section id="menu" className="py-24 max-w-7xl mx-auto px-6 md:px-12">
        <div className="text-center max-w-2xl mx-auto mb-16">
          <span className="text-xs font-semibold uppercase tracking-[0.2em] text-[#b47b2c]">Curated Offerings</span>
          <h2 className="font-['Playfair_Display'] text-3xl md:text-5xl font-bold text-[#1c1c17] mt-3">
            Our Artisanal Menu
          </h2>
          <p className="text-[#5c564a] text-base mt-4">
            From sunrise pour-overs to nourishing midday plates and decadent evening bakes.
          </p>

          {/* Category Filter Tabs */}
          <div className="flex flex-wrap items-center justify-center gap-2 mt-8">
            {['all', 'coffee', 'beverages', 'brunch', 'lunch', 'desserts'].map((tab) => (
              <button
                key={tab}
                onClick={() => setActiveTab(tab)}
                className={`px-5 py-2 rounded-full text-xs font-semibold uppercase tracking-wider transition-all duration-300 ${
                  activeTab === tab
                    ? 'bg-[#1c1c17] text-[#fdf9f1] shadow-sm'
                    : 'bg-[#f0e6d6] text-[#5c564a] hover:bg-[#e4d6c2]'
                }`}
              >
                {tab}
              </button>
            ))}
          </div>
        </div>

        {/* Menu Grid */}
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {filteredMenu.map((item) => (
            <div 
              key={item.id} 
              className="bg-[#f6efe4] rounded-2xl overflow-hidden border border-[#ebdccb] shadow-sm hover:shadow-md transition-all duration-300 flex flex-col group"
            >
              <div className="relative h-56 overflow-hidden">
                <img 
                  src={item.image} 
                  alt={item.name} 
                  className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                />
                <span className="absolute top-4 right-4 bg-[#fdf9f1]/90 backdrop-blur-sm text-[#1c1c17] px-3 py-1 rounded-full text-[10px] font-bold uppercase tracking-wider">
                  {item.badge}
                </span>
              </div>
              <div className="p-6 flex flex-col flex-grow justify-between">
                <div>
                  <div className="flex items-start justify-between gap-4 mb-2">
                    <h3 className="font-['Playfair_Display'] text-xl font-bold text-[#1c1c17]">
                      {item.name}
                    </h3>
                    <span className="font-['Playfair_Display'] text-lg font-bold text-[#b47b2c]">
                      {item.price}
                    </span>
                  </div>
                  <p className="text-sm text-[#5c564a] leading-relaxed">
                    {item.description}
                  </p>
                </div>
                <div className="pt-6 mt-4 border-t border-[#ebdccb] flex items-center justify-between text-xs font-semibold tracking-wider text-[#785a1a] uppercase">
                  <span>Freshly Prepared</span>
                  <span>Order at Counter</span>
                </div>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* ATMOSPHERE / GALLERY */}
      <section id="gallery" className="py-24 bg-[#f4ecdf]">
        <div className="max-w-7xl mx-auto px-6 md:px-12 text-center mb-16">
          <span className="text-xs font-semibold uppercase tracking-[0.2em] text-[#b47b2c]">Visual Journey</span>
          <h2 className="font-['Playfair_Display'] text-3xl md:text-5xl font-bold text-[#1c1c17] mt-3">
            The Aakay Atmosphere
          </h2>
          <p className="text-[#5c564a] text-base mt-4 max-w-xl mx-auto">
            Warm woods, gentle morning light, and curated aesthetics crafted for your comfort.
          </p>
        </div>

        <div className="max-w-7xl mx-auto px-6 md:px-12 grid grid-cols-2 md:grid-cols-3 gap-4 md:gap-6">
          {galleryImages.map((imgUrl, index) => (
            <div key={index} className="overflow-hidden rounded-2xl shadow-sm h-64 md:h-80 group">
              <img 
                src={imgUrl} 
                alt={`Gallery image ${index + 1}`} 
                className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
              />
            </div>
          ))}
        </div>
      </section>

      {/* TESTIMONIALS / REVIEWS */}
      <section id="reviews" className="py-24 max-w-7xl mx-auto px-6 md:px-12">
        <div className="text-center max-w-2xl mx-auto mb-16">
          <span className="text-xs font-semibold uppercase tracking-[0.2em] text-[#b47b2c]">Testimonials</span>
          <h2 className="font-['Playfair_Display'] text-3xl md:text-5xl font-bold text-[#1c1c17] mt-3">
            Words from Our Guests
          </h2>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {[
            {
              quote: "The Ethiopian pour-over is quite simply life-changing. Combined with the truffle sourdough toast, it's my favorite morning ritual in the city.",
              author: "Sophia Sterling",
              role: "Food & Travel Writer"
            },
            {
              quote: "An absolute sanctuary. The ambiance is so calm and beautifully lit, making it the perfect spot for deep work sessions and weekend brunch dates.",
              author: "Liam Henderson",
              role: "Architect & Regular Guest"
            },
            {
              quote: "Incredible hospitality and attention to detail. Every single item we ordered from the brunch menu was cooked to absolute perfection.",
              author: "Ananya Sharma",
              role: "Local Connoisseur"
            }
          ].map((rev, idx) => (
            <div key={idx} className="bg-[#f6efe4] p-8 rounded-2xl border border-[#ebdccb] shadow-sm flex flex-col justify-between">
              <div>
                <div className="flex text-[#b47b2c] mb-4 text-sm">★★★★★</div>
                <p className="text-sm md:text-base text-[#5c564a] italic leading-relaxed">
                  "{rev.quote}"
                </p>
              </div>
              <div className="mt-8 pt-4 border-t border-[#ebdccb]">
                <p className="font-['Playfair_Display'] font-bold text-[#1c1c17]">{rev.author}</p>
                <p className="text-xs text-[#7c7263] uppercase tracking-wider mt-0.5">{rev.role}</p>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* RESERVATIONS SECTION */}
      <section id="reservations" className="py-24 bg-[#1c1c17] text-[#fdf9f1] relative overflow-hidden">
        <div className="max-w-7xl mx-auto px-6 md:px-12 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center relative z-10">
          
          <div className="lg:col-span-5 flex flex-col gap-6">
            <span className="text-xs font-semibold uppercase tracking-[0.2em] text-[#b47b2c]">Table Booking</span>
            <h2 className="font-['Playfair_Display'] text-3xl md:text-5xl font-bold text-[#fdf9f1] leading-tight">
              Reserve Your Experience
            </h2>
            <p className="text-[#a89f91] text-base leading-relaxed">
              Secure your table ahead of time for weekend brunch or intimate evening dining. For large private gatherings, please contact us directly.
            </p>

            <div className="space-y-4 pt-4">
              <div className="flex items-start gap-4">
                <div className="w-8 h-8 rounded-full bg-[#b47b2c]/20 flex items-center justify-center text-[#b47b2c] font-bold text-sm shrink-0">✓</div>
                <div>
                  <p className="font-semibold text-sm">Priority Seating</p>
                  <p className="text-xs text-[#a89f91]">Skip the wait with confirmed reservations.</p>
                </div>
              </div>
              <div className="flex items-start gap-4">
                <div className="w-8 h-8 rounded-full bg-[#b47b2c]/20 flex items-center justify-center text-[#b47b2c] font-bold text-sm shrink-0">✓</div>
                <div>
                  <p className="font-semibold text-sm">Special Requests</p>
                  <p className="text-xs text-[#a89f91]">Dietary adjustments accommodated with care.</p>
                </div>
              </div>
            </div>
          </div>

          <div className="lg:col-span-7 bg-[#272621] p-8 md:p-10 rounded-3xl border border-[#3b3933] shadow-2xl">
            {resSubmitted ? (
              <div className="text-center py-16 flex flex-col items-center gap-4">
                <div className="w-16 h-16 rounded-full bg-[#b47b2c] text-[#fdf9f1] flex items-center justify-center text-2xl font-bold mb-2">✓</div>
                <h3 className="font-['Playfair_Display'] text-2xl font-bold text-[#fdf9f1]">Reservation Confirmed!</h3>
                <p className="text-[#a89f91] text-sm max-w-md">
                  Thank you, <span className="text-[#fdf9f1] font-semibold">{reservation.name}</span>. We have received your booking for <span className="text-[#fdf9f1] font-semibold">{reservation.guests} guests</span> on <span className="text-[#fdf9f1] font-semibold">{reservation.date}</span> at <span className="text-[#fdf9f1] font-semibold">{reservation.time}</span>. A confirmation email has been sent.
                </p>
                <button 
                  onClick={() => setResSubmitted(false)}
                  className="mt-6 bg-[#b47b2c] text-[#fdf9f1] px-6 py-2.5 rounded-full text-xs font-semibold uppercase tracking-wider hover:bg-[#9c6622] transition-colors"
                >
                  Make Another Booking
                </button>
              </div>
            ) : (
              <form onSubmit={handleReservationSubmit} className="space-y-6">
                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Full Name *</label>
                    <input 
                      type="text" 
                      name="name" 
                      value={reservation.name} 
                      onChange={handleInputChange} 
                      placeholder="Jane Doe" 
                      required
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    />
                  </div>
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Email Address *</label>
                    <input 
                      type="email" 
                      name="email" 
                      value={reservation.email} 
                      onChange={handleInputChange} 
                      placeholder="jane@example.com" 
                      required
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    />
                  </div>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Phone Number *</label>
                    <input 
                      type="tel" 
                      name="phone" 
                      value={reservation.phone} 
                      onChange={handleInputChange} 
                      placeholder="+1 (555) 000-0000" 
                      required
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    />
                  </div>
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Number of Guests</label>
                    <select 
                      name="guests" 
                      value={reservation.guests} 
                      onChange={handleInputChange}
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    >
                      <option value="1">1 Person</option>
                      <option value="2">2 Guests</option>
                      <option value="3">3 Guests</option>
                      <option value="4">4 Guests</option>
                      <option value="5">5+ Guests (Large Group)</option>
                    </select>
                  </div>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Date *</label>
                    <input 
                      type="date" 
                      name="date" 
                      value={reservation.date} 
                      onChange={handleInputChange} 
                      required
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    />
                  </div>
                  <div>
                    <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Time Slot</label>
                    <select 
                      name="time" 
                      value={reservation.time} 
                      onChange={handleInputChange}
                      className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                    >
                      <option value="08:00">08:00 AM (Breakfast)</option>
                      <option value="10:00">10:00 AM (Morning Brunch)</option>
                      <option value="12:30">12:30 PM (Lunch)</option>
                      <option value="15:00">03:00 PM (Afternoon Coffee)</option>
                      <option value="18:00">06:00 PM (Evening Dinner)</option>
                      <option value="20:00">08:00 PM (Night Service)</option>
                    </select>
                  </div>
                </div>

                <div>
                  <label className="block text-xs uppercase tracking-wider text-[#a89f91] mb-2 font-medium">Special Requests or Dietary Notes</label>
                  <textarea 
                    name="notes" 
                    value={reservation.notes} 
                    onChange={handleInputChange} 
                    rows="3" 
                    placeholder="Allergies, seating preference, anniversary note..." 
                    className="w-full bg-[#1c1c17] border border-[#3b3933] rounded-xl px-4 py-3 text-sm text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
                  ></textarea>
                </div>

                <button 
                  type="submit" 
                  className="w-full bg-[#b47b2c] text-[#fdf9f1] py-4 rounded-xl text-xs font-semibold uppercase tracking-wider hover:bg-[#9c6622] transition-colors shadow-lg"
                >
                  Confirm Reservation
                </button>
              </form>
            )}
          </div>

        </div>
      </section>

      {/* FOOTER / CONTACT INFO */}
      <footer id="contact" className="bg-[#141411] text-[#a89f91] py-16 border-t border-[#262520]">
        <div className="max-w-7xl mx-auto px-6 md:px-12 grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
          
          <div className="md:col-span-1">
            <a href="#" className="font-['Playfair_Display'] text-2xl font-bold tracking-wider text-[#fdf9f1]">
              AAKAY
            </a>
            <p className="text-xs font-medium tracking-[0.2em] text-[#b47b2c] uppercase mt-1 mb-4">
              Café & Kitchen
            </p>
            <p className="text-xs text-[#a89f91] leading-relaxed">
              Sanctuary of taste offering handcrafted single-origin coffee, artisanal dining, and serene hospitality.
            </p>
          </div>

          <div>
            <p className="font-['Playfair_Display'] text-base font-bold text-[#fdf9f1] mb-4">Hours of Operation</p>
            <ul className="space-y-2 text-xs">
              <li className="flex justify-between"><span>Monday – Friday:</span> <span className="text-[#fdf9f1]">07:30 AM – 10:00 PM</span></li>
              <li className="flex justify-between"><span>Saturday – Sunday:</span> <span className="text-[#fdf9f1]">08:00 AM – 11:00 PM</span></li>
              <li className="text-[11px] text-[#b47b2c] pt-2">Kitchen closes 45 mins prior to closing time.</li>
            </ul>
          </div>

          <div>
            <p className="font-['Playfair_Display'] text-base font-bold text-[#fdf9f1] mb-4">Location & Contact</p>
            <ul className="space-y-2 text-xs">
              <li>42 Artisanal Way, Culinary District</li>
              <li>San Francisco, CA 94107</li>
              <li className="pt-2"><a href="tel:+14155550199" className="hover:text-[#fdf9f1] transition-colors">+1 (415) 555-0199</a></li>
              <li><a href="mailto:hello@aakaycafe.com" className="hover:text-[#fdf9f1] transition-colors">hello@aakaycafe.com</a></li>
            </ul>
          </div>

          <div>
            <p className="font-['Playfair_Display'] text-base font-bold text-[#fdf9f1] mb-4">Newsletter</p>
            <p className="text-xs text-[#a89f91] mb-4">Subscribe to receive secret menu invites and seasonal coffee drops.</p>
            <form onSubmit={(e) => { e.preventDefault(); alert('Subscribed successfully!'); }} className="flex flex-col gap-2">
              <input 
                type="email" 
                placeholder="Your email address" 
                required
                className="bg-[#1c1c17] border border-[#3b3933] rounded-lg px-3 py-2 text-xs text-[#fdf9f1] focus:outline-none focus:border-[#b47b2c]"
              />
              <button 
                type="submit" 
                className="bg-[#b47b2c] text-[#fdf9f1] py-2 rounded-lg text-xs font-semibold uppercase tracking-wider hover:bg-[#9c6622] transition-colors"
              >
                Join
              </button>
            </form>
          </div>

        </div>

        <div className="max-w-7xl mx-auto px-6 md:px-12 pt-8 border-t border-[#262520] flex flex-col sm:flex-row items-center justify-between text-xs text-[#7c7263]">
          <p>© {new Date().getFullYear()} AAKAY Café & Kitchen. All rights reserved.</p>
          <div className="flex gap-6 mt-4 sm:mt-0">
            <a href="#" className="hover:text-[#fdf9f1] transition-colors">Privacy Policy</a>
            <a href="#" className="hover:text-[#fdf9f1] transition-colors">Terms of Service</a>
            <a href="#" className="hover:text-[#fdf9f1] transition-colors">Instagram</a>
          </div>
        </div>
      </footer>

    </div>
  );
}