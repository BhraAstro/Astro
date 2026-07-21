<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>OGEE'S STYLISH '/ Barbershop</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300&family=Outfit:wght@200;300;400;500;600&display=swap" rel="stylesheet"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
<style>
  :root {
    --gold: #c9a84c;
    --gold-light: #e2c97e;
    --gold-dim: rgba(201,168,76,0.15);
    --black: #070707;
    --charcoal: #111111;
    --dark: #181510;
    --card: #161410;
    --border: rgba(201,168,76,0.18);
    --text: #f0ece2;
    --muted: #8a8070;
    --white: #faf8f2;
    --radius: 12px;
    --transition: 0.4s cubic-bezier(0.23,1,0.32,1);
  }

  *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }

  html { scroll-behavior: smooth; font-size:16px; }

  body {
    background: var(--black);
    color: var(--text);
    font-family: 'Outfit', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: none;
  }

  /* ─── CUSTOM CURSOR ─── */
  .cursor {
    width: 10px; height: 10px;
    background: var(--gold);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: width 0.2s, height 0.2s, background 0.2s;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--gold);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.12s, width 0.25s, height 0.25s, opacity 0.25s;
    opacity: 0.6;
  }
  body:hover .cursor { opacity: 1; }

  /* ─── LOADER ─── */
  #loader {
    position: fixed; inset: 0;
    background: var(--black);
    z-index: 10000;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column;
    transition: opacity 0.8s ease, visibility 0.8s ease;
  }
  #loader.hide { opacity: 0; visibility: hidden; }
  .loader-logo {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 6vw, 4rem);
    font-weight: 900;
    letter-spacing: 0.08em;
    color: var(--gold);
    animation: loaderPulse 1.6s ease-in-out infinite;
  }
  .loader-bar {
    margin-top: 24px;
    width: 180px; height: 1px;
    background: var(--border);
    position: relative; overflow: hidden;
  }
  .loader-bar::after {
    content: '';
    position: absolute; left: -100%; top: 0;
    width: 100%; height: 100%;
    background: var(--gold);
    animation: loaderBar 1.5s ease forwards;
  }
  @keyframes loaderBar { to { left: 0; } }
  @keyframes loaderPulse { 0%,100%{opacity:0.5;} 50%{opacity:1;} }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 1000;
    padding: 0 5%;
    height: 72px;
    display: flex; align-items: center; justify-content: space-between;
    background: transparent;
    transition: background var(--transition), backdrop-filter var(--transition);
  }
  nav.scrolled {
    background: rgba(7,7,7,0.92);
    backdrop-filter: blur(18px);
    border-bottom: 1px solid var(--border);
  }
  .nav-brand {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    font-weight: 900;
    letter-spacing: 0.12em;
    color: var(--gold);
    text-decoration: none;
  }
  .nav-brand span { color: var(--white); }
  .nav-links {
    display: flex; gap: 2.5rem; list-style: none;
  }
  .nav-links a {
    font-size: 0.78rem; letter-spacing: 0.18em;
    text-transform: uppercase; font-weight: 400;
    color: var(--muted); text-decoration: none;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px; background: var(--gold);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--gold); }
  .nav-links a:hover::after { width: 100%; }
  .nav-cta {
    background: var(--gold);
    color: var(--black) !important;
    padding: 8px 20px;
    border-radius: 3px;
    font-weight: 600 !important;
    letter-spacing: 0.12em !important;
    transition: background 0.3s, transform 0.3s !important;
  }
  .nav-cta:hover { background: var(--gold-light) !important; transform: translateY(-2px); }
  .nav-cta::after { display: none !important; }
  .hamburger {
    display: none; flex-direction: column; gap: 5px;
    cursor: pointer; padding: 4px;
  }
  .hamburger span {
    display: block; width: 24px; height: 1.5px;
    background: var(--gold); transition: var(--transition);
  }
  .mobile-menu {
    display: none;
    position: fixed; inset: 0;
    background: rgba(7,7,7,0.98);
    z-index: 999;
    flex-direction: column; align-items: center; justify-content: center;
    gap: 2rem;
  }
  .mobile-menu.open { display: flex; }
  .mobile-menu a {
    font-family: 'Playfair Display', serif;
    font-size: 2rem; font-weight: 700;
    color: var(--text); text-decoration: none;
    transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--gold); }

  /* ─── HERO ─── */
  #hero {
    position: relative; height: 100vh; min-height: 620px;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse at 70% 40%, rgba(201,168,76,0.07) 0%, transparent 60%),
      linear-gradient(160deg, #0a0805 0%, #070707 60%, #0d0b08 100%);
  }
  .hero-pattern {
    position: absolute; inset: 0;
    background-image:
      repeating-linear-gradient(
        45deg,
        transparent,
        transparent 48px,
        rgba(201,168,76,0.03) 48px,
        rgba(201,168,76,0.03) 49px
      );
  }
  .hero-image-overlay {
    position: absolute; inset: 0;
    background: url('images/IMG_9519.PNG') center/cover no-repeat;
    opacity: 0.40;
    filter: grayscale(40%);
  }
  .hero-content {
    position: relative; z-index: 2;
    text-align: center; padding: 0 5%;
    max-width: 900px;
  }
  .hero-badge {
    display: inline-block;
    font-size: 0.7rem; letter-spacing: 0.35em;
    text-transform: uppercase; color: var(--gold);
    border: 1px solid var(--border);
    padding: 6px 20px; margin-bottom: 2rem;
    font-weight: 400;
    opacity: 0;
    animation: fadeUp 0.8s 1.8s forwards;
  }
  .hero-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 8vw, 7.5rem);
    font-weight: 900;
    line-height: 0.95;
    letter-spacing: -0.02em;
    color: var(--gold);
    opacity: 0;
    animation: fadeUp 0.9s 2s forwards;
  }
  .hero-title em {
    font-style: italic;
    color: var(--white);
    display: block;
  }
  .hero-sub {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1rem, 2.2vw, 1.35rem);
    font-weight: 300;
    font-style: italic;
    color: var(--muted);
    margin-top: 1.5rem;
    letter-spacing: 0.04em;
    opacity: 0;
    animation: fadeUp 0.9s 2.2s forwards;
  }
  .hero-buttons {
    display: flex; gap: 1rem; justify-content: center;
    margin-top: 2.8rem; flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.9s 2.5s forwards;
  }
  .btn-primary {
    background: var(--gold);
    color: var(--black);
    padding: 14px 36px;
    font-size: 0.8rem; letter-spacing: 0.2em;
    text-transform: uppercase; font-weight: 600;
    border: none; border-radius: 3px;
    cursor: pointer; text-decoration: none;
    transition: background 0.3s, transform 0.3s, box-shadow 0.3s;
    display: inline-flex; align-items: center; gap: 10px;
  }
  .btn-primary:hover {
    background: var(--gold-light);
    transform: translateY(-3px);
    box-shadow: 0 12px 30px rgba(201,168,76,0.25);
  }
  .btn-outline {
    background: transparent;
    color: var(--text);
    padding: 13px 36px;
    font-size: 0.8rem; letter-spacing: 0.2em;
    text-transform: uppercase; font-weight: 400;
    border: 1px solid var(--border);
    border-radius: 3px;
    cursor: pointer; text-decoration: none;
    transition: border-color 0.3s, color 0.3s, transform 0.3s;
    display: inline-flex; align-items: center; gap: 10px;
  }
  .btn-outline:hover {
    border-color: var(--gold);
    color: var(--gold);
    transform: translateY(-3px);
  }
  .hero-scroll {
    position: absolute; bottom: 2.5rem; left: 50%;
    transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    opacity: 0;
    animation: fadeUp 0.9s 3s forwards;
  }
  .hero-scroll span {
    font-size: 0.65rem; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--muted);
  }
  .scroll-line {
    width: 1px; height: 44px;
    background: linear-gradient(to bottom, var(--gold), transparent);
    animation: scrollDown 1.8s ease-in-out infinite;
  }
  @keyframes scrollDown {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    51% { transform: scaleY(1); transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ─── SECTION COMMON ─── */
  section { padding: 100px 5%; }
  .section-label {
    font-size: 0.68rem; letter-spacing: 0.35em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-bottom: 1rem;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4.5vw, 3.5rem);
    font-weight: 700; line-height: 1.1;
    color: var(--white);
  }
  .section-title em { font-style: italic; color: var(--gold); }
  .section-divider {
    width: 60px; height: 1px; background: var(--gold);
    margin: 1.5rem 0; opacity: 0.6;
  }
  .section-center { text-align: center; }
  .section-center .section-divider { margin: 1.5rem auto; }

  /* ─── SERVICES ─── */
  #services { background: var(--charcoal); }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1.5rem; margin-top: 3.5rem;
  }
  .service-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 2.2rem 1.8rem;
    position: relative; overflow: hidden;
    transition: transform var(--transition), border-color var(--transition), box-shadow var(--transition);
  }
  .service-card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    opacity: 0; transition: opacity var(--transition);
  }
  .service-card:hover {
    transform: translateY(-8px);
    border-color: rgba(201,168,76,0.4);
    box-shadow: 0 20px 50px rgba(0,0,0,0.5), 0 0 30px rgba(201,168,76,0.06);
  }
  .service-card:hover::before { opacity: 1; }
  .service-icon {
    width: 54px; height: 54px;
    background: var(--gold-dim);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 1.4rem;
    font-size: 1.4rem; color: var(--gold);
    transition: background var(--transition);
  }
  .service-card:hover .service-icon { background: rgba(201,168,76,0.25); }
  .service-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.25rem; font-weight: 700;
    color: var(--white); margin-bottom: 0.6rem;
  }
  .service-desc {
    font-size: 0.85rem; color: var(--muted);
    line-height: 1.7; margin-bottom: 1.4rem;
  }
  .service-footer {
    display: flex; align-items: center; justify-content: space-between;
  }
  .service-price {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.6rem; font-weight: 600;
    color: var(--gold);
  }
  .service-duration {
    font-size: 0.72rem; letter-spacing: 0.12em;
    color: var(--muted); text-transform: uppercase;
  }
  .service-vip {
    position: absolute; top: 1rem; right: 1rem;
    background: var(--gold);
    color: var(--black);
    font-size: 0.6rem; letter-spacing: 0.2em;
    text-transform: uppercase; font-weight: 700;
    padding: 3px 10px; border-radius: 20px;
  }

  /* ─── ABOUT ─── */
  #about {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6rem; align-items: center;
    background: var(--black);
  }
  .about-image-wrap {
    position: relative;
  }
  .about-img {
    width: 100%; aspect-ratio: 4/5;
    object-fit: cover; border-radius: var(--radius);
    filter: grayscale(20%) brightness(0.85);
    transition: filter 0.5s;
  }
  .about-img:hover { filter: grayscale(0%) brightness(2.95); }
  .about-img-placeholder {
    width: 100%; aspect-ratio: 4/5;
    background: url('images/IMG_9519.PNG') center/cover;
    border-radius: var(--radius);
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-size: 5rem; color: var(--gold);
  }
  .about-badge {
    position: absolute; bottom: -1.5rem; right: -1.5rem;
    width: 130px; height: 130px;
    background: var(--gold);
    border-radius: 50%;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    box-shadow: 0 8px 30px rgba(201,168,76,0.3);
  }
  .about-badge-num {
    font-family: 'Playfair Display', serif;
    font-size: 2.4rem; font-weight: 900;
    color: var(--black); line-height: 1;
  }
  .about-badge-text {
    font-size: 0.6rem; letter-spacing: 0.15em;
    text-transform: uppercase; color: var(--black);
    font-weight: 600; text-align: center;
    margin-top: 2px;
  }
  .about-stats {
    display: flex; gap: 2.5rem; margin: 2.5rem 0;
  }
  .stat { text-align: center; }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem; font-weight: 700; color: var(--gold);
    line-height: 1;
  }
  .stat-label {
    font-size: 0.72rem; color: var(--muted);
    text-transform: uppercase; letter-spacing: 0.15em;
    margin-top: 4px;
  }
  .about-text {
    font-size: 0.95rem; color: var(--muted);
    line-height: 1.9; margin: 1rem 0 2rem;
  }

  /* ─── TEAM ─── */
  #team { background: var(--charcoal); }
  .team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 2rem; margin-top: 3.5rem;
  }
  .team-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
    transition: transform var(--transition), box-shadow var(--transition);
  }
  .team-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 50px rgba(0,0,0,0.5);
  }
  .team-img-wrap1 {
    aspect-ratio: 3/3;
    background: url('images/IMG_9519.PNG') center/cover no-repeat;
    font-size: 4rem; color: rgba(201,168,76,0.2);
    position: relative; overflow: hidden;
  }
  .team-img-wrap2 {
    aspect-ratio: 3/3;
    background: url('images/IMG_9519.PNG') center/cover no-repeat;
    font-size: 4rem; color: rgba(201,168,76,0.2);
    position: relative; overflow: hidden;
  }

  .team-img-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, var(--card) 0%, transparent 50%);
  }
  .team-info1 { padding: 1.4rem; }
  .team-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.15rem; font-weight: 700;
    color: var(--white);
  }
  .team-info2 { padding: 1.4rem; }
  .team-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.15rem; font-weight: 700;
    color: var(--white);
  }

  .team-role {
    font-size: 0.75rem; color: var(--gold);
    letter-spacing: 0.15em; text-transform: uppercase;
    margin-top: 3px;
  }
  .team-socials {
    display: flex; gap: 0.8rem; margin-top: 1rem;
  }
  .team-socials a {
    width: 30px; height: 30px;
    border: 1px solid var(--border);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    color: var(--muted); font-size: 0.75rem;
    text-decoration: none; transition: all 0.3s;
  }
  .team-socials a:hover {
    border-color: var(--gold); color: var(--gold);
  }

  /* ─── GALLERY ─── */
  #gallery { background: var(--black); }
  .gallery-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: auto;
    gap: 0.8rem;
    margin-top: 3.5rem;
  }
  .gallery-item {
    position: relative; overflow: hidden;
    border-radius: 8px;
    aspect-ratio: 1;
    cursor: pointer;
  }
  .gallery-item:nth-child(1) { grid-row: span 2; aspect-ratio: unset; }
  .gallery-item:nth-child(4) { grid-column: span 2; aspect-ratio: 2/1; }
  .gallery-thumb {
    width: 100%; height: 100%;
    object-fit: cover;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1), filter 0.4s;
    filter: grayscale(20%) brightness(0.8);
  }
  .gallery-item-bg1 {
    width: 100%; height: 100%;
    background: url('images/IMG_9519.PNG') center/cover no-repeat;
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item-bg2 {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #1a1510, #0d0b08);
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item-bg3 {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #1a1510, #0d0b08);
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item-bg4 {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #1a1510, #0d0b08);
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item-bg5 {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #1a1510, #0d0b08);
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item-bg6 {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #1a1510, #0d0b08);
    display: flex; align-items: center; justify-content: center;
    color: rgba(201,168,76,0.15); font-size: 4rem;
    transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
  }
  .gallery-item:hover .gallery-thumb,
  .gallery-item:hover .gallery-item-bg {
    transform: scale(1.08);
    filter: grayscale(0%) brightness(0.9);
  }
  .gallery-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.7) 0%, transparent 60%);
    opacity: 0; transition: opacity 0.4s;
    display: flex; align-items: flex-end; padding: 1.5rem;
  }
  .gallery-item:hover .gallery-overlay { opacity: 1; }
  .gallery-tag {
    font-size: 0.72rem; letter-spacing: 0.2em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 500;
  }

  /* ─── BOOKING ─── */
  #booking { background: var(--charcoal); }
  .booking-wrap {
    display: grid;
    grid-template-columns: 1fr 1.4fr;
    gap: 5rem; align-items: start;
    margin-top: 3.5rem;
  }
  .booking-info p {
    font-size: 0.9rem; color: var(--muted);
    line-height: 1.8; margin-bottom: 2rem;
  }
  .booking-detail {
    display: flex; align-items: flex-start; gap: 1rem;
    margin-bottom: 1.4rem;
  }
  .booking-detail-icon {
    width: 38px; height: 38px; min-width: 38px;
    background: var(--gold-dim);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    color: var(--gold); font-size: 0.9rem;
  }
  .booking-detail-text strong {
    display: block; color: var(--text);
    font-size: 0.85rem; font-weight: 500;
  }
  .booking-detail-text span {
    font-size: 0.8rem; color: var(--muted);
  }
  .booking-form {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 2.5rem;
  }
  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
  }
  .form-group { margin-bottom: 1.3rem; }
  .form-group label {
    display: block; font-size: 0.72rem;
    letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--muted); margin-bottom: 8px; font-weight: 400;
  }
  .form-group input,
  .form-group select,
  .form-group textarea {
    width: 100%;
    background: rgba(255,255,255,0.04);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 12px 15px;
    color: var(--text); font-family: 'Outfit', sans-serif;
    font-size: 0.9rem; font-weight: 300;
    outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
    appearance: none;
  }
  .form-group select {
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%238a8070' fill='none' stroke-width='1.5'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 14px center;
    padding-right: 36px;
  }
  .form-group input:focus,
  .form-group select:focus,
  .form-group textarea:focus {
    border-color: var(--gold);
    box-shadow: 0 0 0 3px rgba(201,168,76,0.08);
  }
  .form-group input::placeholder,
  .form-group textarea::placeholder { color: rgba(138,128,112,0.5); }
  .form-group option { background: #1a1510; }
  .form-submit {
    width: 100%; padding: 15px;
    background: var(--gold); color: var(--black);
    border: none; border-radius: 6px;
    font-family: 'Outfit', sans-serif;
    font-size: 0.82rem; letter-spacing: 0.22em;
    text-transform: uppercase; font-weight: 600;
    cursor: pointer; margin-top: 0.5rem;
    transition: background 0.3s, transform 0.3s, box-shadow 0.3s;
  }
  .form-submit:hover {
    background: var(--gold-light);
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(201,168,76,0.25);
  }

  /* ─── TESTIMONIALS ─── */
  #testimonials { background: var(--black); }
  .testimonials-slider {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem; margin-top: 3.5rem;
  }
  .testimonial-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 2rem;
    transition: transform var(--transition), border-color var(--transition);
  }
  .testimonial-card:hover {
    transform: translateY(-6px);
    border-color: rgba(201,168,76,0.35);
  }
  .testimonial-stars {
    color: var(--gold); font-size: 0.85rem;
    letter-spacing: 3px; margin-bottom: 1.2rem;
  }
  .testimonial-text {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.05rem; font-style: italic;
    color: var(--text); line-height: 1.75;
    margin-bottom: 1.5rem;
  }
  .testimonial-author {
    display: flex; align-items: center; gap: 1rem;
  }
  .author-avatar {
    width: 44px; height: 44px; border-radius: 50%;
    background: var(--gold-dim);
    border: 2px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Playfair Display', serif;
    font-weight: 700; color: var(--gold); font-size: 1rem;
  }
  .author-info strong {
    display: block; color: var(--white); font-size: 0.9rem;
  }
  .author-info span {
    font-size: 0.75rem; color: var(--muted);
  }
  .quote-mark {
    font-family: 'Playfair Display', serif;
    font-size: 5rem; color: var(--gold);
    opacity: 0.15; line-height: 0.8;
    margin-bottom: -1rem; display: block;
  }

  /* ─── CONTACT ─── */
  #contact { background: var(--charcoal); }
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1.2fr;
    gap: 4rem; margin-top: 3.5rem;
  }
  .contact-info-items { margin-top: 1.5rem; }
  .contact-item {
    display: flex; align-items: flex-start;
    gap: 1.2rem; margin-bottom: 1.8rem;
  }
  .contact-icon {
    width: 44px; height: 44px; min-width: 44px;
    background: var(--gold-dim);
    border: 1px solid var(--border);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    color: var(--gold); font-size: 1rem;
  }
  .contact-item-text strong {
    display: block; color: var(--white);
    font-size: 0.85rem; font-weight: 500;
    margin-bottom: 3px;
  }
  .contact-item-text span {
    font-size: 0.82rem; color: var(--muted); line-height: 1.6;
  }
  .social-links {
    display: flex; gap: 0.8rem; margin-top: 2rem;
  }
  .social-link {
    width: 42px; height: 42px;
    background: var(--gold-dim);
    border: 1px solid var(--border);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    color: var(--muted); font-size: 1rem;
    text-decoration: none; transition: all 0.3s;
  }
  .social-link:hover {
    background: var(--gold);
    border-color: var(--gold);
    color: var(--black);
    transform: translateY(-3px);
  }
  .map-container {
    border-radius: var(--radius);
    overflow: hidden;
    border: 1px solid var(--border);
    height: 100%;
    min-height: 350px;
    background: #111;
    display: flex; align-items: center; justify-content: center;
    color: var(--muted); font-size: 0.85rem;
    flex-direction: column; gap: 1rem;
  }
  .map-container iframe {
    width: 100%; height: 100%;
    min-height: 350px;
    filter: grayscale(60%) brightness(0.7) sepia(20%);
    border: none;
  }

  /* ─── FOOTER ─── */
  footer {
    background: #050505;
    border-top: 1px solid var(--border);
    padding: 3rem 5%;
    display: flex;
    align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 1.5rem;
  }
  .footer-brand {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem; font-weight: 900;
    letter-spacing: 0.1em; color: var(--gold);
  }
  .footer-brand span { color: var(--white); }
  .footer-copy {
    font-size: 0.78rem; color: var(--muted);
    letter-spacing: 0.05em;
  }
  .footer-links {
    display: flex; gap: 2rem;
  }
  .footer-links a {
    font-size: 0.75rem; color: var(--muted);
    text-decoration: none; letter-spacing: 0.1em;
    text-transform: uppercase; transition: color 0.3s;
  }
  .footer-links a:hover { color: var(--gold); }

  /* ─── FLOATING BOOK BUTTON ─── */
  .float-btn {
    position: fixed; right: 2rem; bottom: 2rem;
    z-index: 999;
    background: var(--gold);
    color: var(--black);
    padding: 14px 22px;
    border-radius: 50px;
    font-family: 'Outfit', sans-serif;
    font-size: 0.78rem; letter-spacing: 0.18em;
    text-transform: uppercase; font-weight: 700;
    text-decoration: none;
    box-shadow: 0 8px 30px rgba(201,168,76,0.35);
    transition: all 0.3s;
    display: flex; align-items: center; gap: 8px;
    animation: floatPulse 3s ease-in-out infinite;
  }
  .float-btn:hover {
    background: var(--gold-light);
    transform: scale(1.05) translateY(-3px);
    box-shadow: 0 14px 40px rgba(201,168,76,0.45);
  }
  @keyframes floatPulse {
    0%,100%{ box-shadow: 0 8px 30px rgba(201,168,76,0.35); }
    50%{ box-shadow: 0 8px 40px rgba(201,168,76,0.55); }
  }

  /* ─── SCROLL REVEAL ─── */
  .reveal {
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 900px) {
    #about { grid-template-columns: 1fr; gap: 3rem; }
    .about-badge { bottom: -1rem; right: 0.5rem; }
    .booking-wrap { grid-template-columns: 1fr; gap: 3rem; }
    .contact-grid { grid-template-columns: 1fr; gap: 3rem; }
    .gallery-grid { grid-template-columns: 1fr 1fr; }
    .gallery-item:nth-child(1) { grid-row: span 1; aspect-ratio: 1; }
    .gallery-item:nth-child(4) { grid-column: span 1; aspect-ratio: 1; }
    .nav-links { display: none; }
    .hamburger { display: flex; }
  }
  @media (max-width: 600px) {
    section { padding: 70px 5%; }
    .form-row { grid-template-columns: 1fr; }
    .gallery-grid { grid-template-columns: 1fr; }
    .gallery-item:nth-child(4) { grid-column: span 1; }
    footer { flex-direction: column; text-align: center; }
    .about-stats { flex-wrap: wrap; gap: 1.5rem; }
    .hero-buttons { flex-direction: column; align-items: center; }
  }
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- LOADER -->
<div id="loader">
  <div class="loader-logo">OGEE'S</div>
  <div class="loader-bar"></div>
</div>

<!-- FLOATING BOOK BUTTON -->
<a href="#booking" class="float-btn">
  <i class="fa-solid fa-scissors"></i> Book Now
</a>

<!-- NAVBAR -->
<nav id="navbar">
  <a href="#hero" class="nav-brand">OGEE'S <span>STYLISH CUT</span></a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#team">Team</a></li>
    <li><a href="#gallery">Gallery</a></li>
    <li><a href="#testimonials">Reviews</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#booking" class="nav-cta">Book Now</a></li>
  </ul>
  <div class="hamburger" id="hamburger">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#services" onclick="closeMobile()">Services</a>
  <a href="#about" onclick="closeMobile()">About</a>
  <a href="#team" onclick="closeMobile()">Team</a>
  <a href="#gallery" onclick="closeMobile()">Gallery</a>
  <a href="#testimonials" onclick="closeMobile()">Reviews</a>
  <a href="#contact" onclick="closeMobile()">Contact</a>
  <a href="#booking" onclick="closeMobile()" style="color:var(--gold)">Book Now</a>
</div>

<!-- ─── HERO ─── -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-pattern"></div>
  <div class="hero-image-overlay"></div>
  <div class="hero-content">
    <div class="hero-badge">Tema. 2026 &nbsp;·&nbsp; Premium Barbershop</div>
    <h1 class="hero-title">
       OGEE'S.<br><em>Timeless Style.</em>
    </h1>
    <p class="hero-sub">
      Where every visit is a ritual, and every cut tells your story.
    </p>
    <div class="hero-buttons">
      <a href="#booking" class="btn-primary">
        <i class="fa-regular fa-calendar"></i> Book Appointment
      </a>
      <a href="#services" class="btn-outline">
        View Services <i class="fa-solid fa-arrow-right"></i>
      </a>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ─── SERVICES ─── -->
<section id="services">
  <div class="section-center">
    <p class="section-label reveal">What We Offer</p>
    <h2 class="section-title reveal reveal-delay-1">Our <em>Services</em></h2>
    <div class="section-divider"></div>
    <p style="color:var(--muted);font-size:0.9rem;max-width:520px;margin:0 auto;line-height:1.8;" class="reveal reveal-delay-2">
      Every service is delivered with precision, care, and that signature Ogee's touch.
    </p>
  </div>
  <div class="services-grid">
    <div class="service-card reveal">
      <div class="service-icon"><i class="fa-solid fa-scissors"></i></div>
      <div class="service-name">Classic Haircut</div>
      <div class="service-desc">A timeless cut tailored to your face shape, with precision blending and a clean finish that turns heads.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 60</div>
        <div class="service-duration">45 mins</div>
      </div>
    </div>
    <div class="service-card reveal reveal-delay-1">
      <div class="service-icon"><i class="fa-solid fa-user-tie"></i></div>
      <div class="service-name">Beard Grooming</div>
      <div class="service-desc">Sculpt, shape, and define your beard to perfection. Hot towel treatment and premium oils included.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 45</div>
        <div class="service-duration">30 mins</div>
      </div>
    </div>
    <div class="service-card reveal reveal-delay-2">
      <div class="service-icon"><i class="fa-solid fa-spa"></i></div>
      <div class="service-name">Luxury Shave</div>
      <div class="service-desc">A straight-razor hot shave with pre-shave oil, hot towels, and a soothing post-shave balm ritual.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 55</div>
        <div class="service-duration">40 mins</div>
      </div>
    </div>
    <div class="service-card reveal reveal-delay-3">
      <div class="service-icon"><i class="fa-solid fa-crown"></i></div>
      <div class="service-name">Cut + Beard Combo</div>
      <div class="service-desc">The full package — a precision haircut paired with expert beard grooming. Looking sharp from top to bottom.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 95</div>
        <div class="service-duration">75 mins</div>
      </div>
    </div>
    <div class="service-card reveal reveal-delay-1">
      <span class="service-vip">VIP</span>
      <div class="service-icon"><i class="fa-solid fa-star"></i></div>
      <div class="service-name">VIP Signature Package</div>
      <div class="service-desc">The full luxury experience: cut, shave, beard, scalp massage, face steam, and a premium drink on arrival.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 180</div>
        <div class="service-duration">2 hrs</div>
      </div>
    </div>
    <div class="service-card reveal reveal-delay-2">
      <div class="service-icon"><i class="fa-solid fa-child"></i></div>
      <div class="service-name">Kids Cut</div>
      <div class="service-desc">A gentle, fun experience for young gentlemen. Patient barbers, cool designs, and a great first memory.</div>
      <div class="service-footer">
        <div class="service-price">GH₵ 40</div>
        <div class="service-duration">30 mins</div>
      </div>
    </div>
  </div>
</section>

<!-- ─── ABOUT ─── -->
<section id="about">
  <div class="about-image-wrap reveal">
    <div class="about-img-placeholder"><i class="fa-solid fa-scissors"></i></div>
    <div class="about-badge">
      <div class="about-badge-num">10+</div>
      <div class="about-badge-text">Years of<br>Excellence</div>
    </div>
  </div>
  <div>
    <p class="section-label reveal">Our Story</p>
    <h2 class="section-title reveal reveal-delay-1">More Than a Cut,<br><em>It's an Experience.</em></h2>
    <div class="section-divider"></div>
    <p class="about-text reveal reveal-delay-2">
      Born in the streets of Koforidua, OGEE'S STYLISH CUT began as a single chair and a relentless passion for the craft. Today, it stands as the city's most trusted destination for men who demand more from their barber — not just a cut, but a ritual.
    </p>
    <p class="about-text reveal reveal-delay-2">
      Every barber on our team is certified, experienced, and devoted to the art of grooming. We blend classic techniques with modern trends to create styles that are as unique as the men who wear them.
    </p>
    <div class="about-stats reveal reveal-delay-3">
      <div class="stat">
        <div class="stat-num">5K+</div>
        <div class="stat-label">Happy Clients</div>
      </div>
      <div class="stat">
        <div class="stat-num">8</div>
        <div class="stat-label">Expert Barbers</div>
      </div>
      <div class="stat">
        <div class="stat-num">4.9★</div>
        <div class="stat-label">Rating</div>
      </div>
    </div>
    <a href="#booking" class="btn-primary reveal reveal-delay-4" style="display:inline-flex;">
      <i class="fa-regular fa-calendar"></i> Book Your Session
    </a>
  </div>
</section>

<!-- ─── TEAM ─── -->
<section id="team">
  <div class="section-center">
    <p class="section-label reveal">The Craftsmen</p>
    <h2 class="section-title reveal reveal-delay-1">Meet <em>The Team</em></h2>
    <div class="section-divider"></div>
    <p style="color:var(--muted);font-size:0.9rem;max-width:500px;margin:0 auto;line-height:1.8;" class="reveal reveal-delay-2">
      Passionate, skilled, and dedicated — our barbers are artists who treat every head as their canvas.
    </p>
  </div>
  <div class="team-grid">
    <div class="team-card reveal">
      <div class="team-img-wrap1">
        <i class="fa-solid fa-user"></i>
        <div class="team-img-overlay"></div>
      </div>
      <div class="team-info1">
        <div class="team-name">kweku Dovlo</div>
        <div class="team-role">Founder & Master Barber</div>
        <div class="team-socials">
          <a href="#"><i class="fa-brands fa-instagram"></i></a>
          <a href="#"><i class="fa-brands fa-tiktok"></i></a>
          <a href="#"><i class="fa-brands fa-x-twitter"></i></a>
          <a href="#"><i class="fa-brands fa-facebook-f"></i></a>
          <a href="#"><i class="fa-brands fa-whatsapp"></i></a>
        </div>
      </div>
    </div>
    <div class="team-card reveal reveal-delay-1">
      <div class="team-img-wrap2">
        <i class="fa-solid fa-user"></i>
        <div class="team-img-overlay"></div>
      </div>
      <div class="team-info2">
        <div class="team-name">Marcus Asante</div>
        <div class="team-role">Assistant Stylist</div>
        <div class="team-socials">
          <a href="#"><i class="fa-brands fa-instagram"></i></a>
          <a href="#"><i class="fa-brands fa-tiktok"></i></a>
          <a href="#"><i class="fa-brands fa-x-twitter"></i></a>
          <a href="#"><i class="fa-brands fa-facebook-f"></i></a>
          <a href="#"><i class="fa-brands fa-whatsapp"></i></a>
        </div>
      </div>
  </div>
</section>

<!-- ─── GALLERY ─── -->
<section id="gallery">
  <div class="section-center">
    <p class="section-label reveal">Our Work</p>
    <h2 class="section-title reveal reveal-delay-1">The <em>Gallery</em></h2>
    <div class="section-divider"></div>
  </div>
  <div class="gallery-grid">
    <div class="gallery-item reveal">
      <div class="gallery-item-bg1"><i class="fa-solid fa-scissors"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Signature Fade</span></div>
    </div>
    <div class="gallery-item reveal reveal-delay-1">
      <div class="gallery-item-bg2"><i class="fa-solid fa-user-tie"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Classic Taper</span></div>
    </div>
    <div class="gallery-item reveal reveal-delay-2">
      <div class="gallery-item-bg3"><i class="fa-solid fa-star"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Beard Design</span></div>
    </div>
    <div class="gallery-item reveal reveal-delay-1">
      <div class="gallery-item-bg4"><i class="fa-solid fa-crown"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Bald Fade</span></div>
    </div>
    <div class="gallery-item reveal reveal-delay-2">
      <div class="gallery-item-bg5"><i class="fa-solid fa-spa"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Hot Shave</span></div>
    </div>
    <div class="gallery-item reveal reveal-delay-3">
      <div class="gallery-item-bg6"><i class="fa-solid fa-store"></i></div>
      <div class="gallery-overlay"><span class="gallery-tag">Shop Vibes</span></div>
    </div>
  </div>
</section>

<!-- ─── BOOKING ─── -->
<section id="booking">
  <p class="section-label reveal">Reserve Your Spot</p>
  <h2 class="section-title reveal reveal-delay-1">Book an <em>Appointment</em></h2>
  <div class="section-divider"></div>
  <div class="booking-wrap">
    <div class="booking-info reveal">
      <p>Skip the wait. Book your preferred barber and service online, and walk in ready to be transformed.</p>
      <div class="booking-detail">
        <div class="booking-detail-icon"><i class="fa-regular fa-clock"></i></div>
        <div class="booking-detail-text">
          <strong>Working Hours</strong>
          <span>Mon – Fri: 8:00 AM – 8:00 PM<br>Sat – Sun: 9:00 AM – 6:00 PM</span>
        </div>
      </div>
      <div class="booking-detail">
        <div class="booking-detail-icon"><i class="fa-solid fa-location-dot"></i></div>
        <div class="booking-detail-text">
          <strong>Location</strong>
          <span>Tema Community 25 Dawhenya, Tarrazzo Junction <br>Greater Accra, Ghana</span>
        </div>
      </div>
      <div class="booking-detail">
        <div class="booking-detail-icon"><i class="fa-solid fa-phone"></i></div>
        <div class="booking-detail-text">
          <strong>Phone</strong>
          <span>+233 (0) 24 000 0000</span>
        </div>
      </div>
    </div>
    <div class="booking-form reveal reveal-delay-2">
      <div class="form-row">
        <div class="form-group">
          <label>First Name</label>
          <input type="text" placeholder="Ogee's" />
        </div>
        <div class="form-group">
          <label>Last Name</label>
          <input type="text" placeholder="Dovlo" />
        </div>
      </div>
      <div class="form-group">
        <label>Phone Number</label>
        <input type="tel" placeholder="+233 24 000 0000" />
      </div>
      <div class="form-group">
        <label>Select Service</label>
        <select>
          <option value="">Choose a service...</option>
          <option>Classic Haircut — GH₵ 30</option>
          <option>Beard Grooming — GH₵ 45</option>
          <option>Luxury Shave — GH₵ 55</option>
          <option>Cut + Beard Combo — GH₵ 95</option>
          <option>VIP Signature Package — GH₵ 180</option>
          <option>Kids Cut — GH₵ 30</option>
        </select>
      </div>
      <div class="form-group">
        <label>Select Barber</label>
        <select>
          <option value="">Any available barber</option>
          <option>Kweku Dovlo (Master Barber)</option>
          <option>Marcus Asante (Senior Stylist)</option>
          </select>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Date</label>
          <input type="date" />
        </div>
        <div class="form-group">
          <label>Preferred Time</label>
          <select>
            <option>08:00 AM</option>
            <option>09:00 AM</option>
            <option>10:00 AM</option>
            <option>11:00 AM</option>
            <option>12:00 PM</option>
            <option>01:00 PM</option>
            <option>02:00 PM</option>
            <option>03:00 PM</option>
            <option>04:00 PM</option>
            <option>05:00 PM</option>
            <option>06:00 PM</option>
          </select>
        </div>
      </div>
      <button class="form-submit" onclick="handleBooking()">
        Confirm Appointment <i class="fa-solid fa-arrow-right" style="margin-left:8px"></i>
      </button>
    </div>
  </div>
</section>

<!-- ─── TESTIMONIALS ─── -->
<section id="testimonials">
  <div class="section-center">
    <p class="section-label reveal">What Clients Say</p>
    <h2 class="section-title reveal reveal-delay-1">Real <em>Reviews</em></h2>
    <div class="section-divider"></div>
  </div>
  <div class="testimonials-slider">
    <div class="testimonial-card reveal">
      <span class="quote-mark">"</span>
      <div class="testimonial-stars">★★★★★</div>
      <div class="testimonial-text">Ogee's is not just a barbershop — it's therapy. The atmosphere, the attention to detail, and Ogee himself are absolutely world-class. I drive 40 minutes just to come here.</div>
      <div class="testimonial-author">
        <div class="author-avatar">KB</div>
        <div class="author-info">
          <strong>Bhra Astro</strong>
          <span>Regular Client · 5 years</span>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal reveal-delay-1">
      <span class="quote-mark">"</span>
      <div class="testimonial-stars">★★★★★</div>
      <div class="testimonial-text">The VIP package is worth every pesewa. Hot towel, scalp massage, a cold drink — and the cleanest fade I've ever had. This is luxury barbering done right in Koforidua.</div>
      <div class="testimonial-author">
        <div class="author-avatar">EA</div>
        <div class="author-info">
          <strong>Emmanuel Asante</strong>
          <span>VIP Package Client</span>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal reveal-delay-2">
      <span class="quote-mark">"</span>
      <div class="testimonial-stars">★★★★★</div>
      <div class="testimonial-text">Marcus understood my vision immediately and executed it perfectly. My beard has never looked this sharp. The whole team has that rare mix of skill and genuine passion.</div>
      <div class="testimonial-author">
        <div class="author-avatar">AP</div>
        <div class="author-info">
          <strong>Amos Prempeh</strong>
          <span>Beard Specialist Client</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ─── CONTACT ─── -->
<section id="contact">
  <p class="section-label reveal">Find Us</p>
  <h2 class="section-title reveal reveal-delay-1">Get in <em>Touch</em></h2>
  <div class="section-divider"></div>
  <div class="contact-grid">
    <div>
      <p style="color:var(--muted);font-size:0.9rem;line-height:1.8;" class="reveal">
        We're conveniently located in the heart of Tema. Walk-ins welcome, appointments always preferred.
      </p>
      <div class="contact-info-items">
        <div class="contact-item reveal reveal-delay-1">
          <div class="contact-icon"><i class="fa-solid fa-location-dot"></i></div>
          <div class="contact-item-text">
            <strong>Address</strong>
            <span>Tema, Community 25 Dawhenya, Tarrazzo Junction <br>Greater Accra, Ghana</span>
          </div>
        </div>
        <div class="contact-item reveal reveal-delay-2">
          <div class="contact-icon"><i class="fa-solid fa-phone"></i></div>
          <div class="contact-item-text">
            <strong>Phone</strong>
            <span>+233 (0) 25 4152 4397</span>
          </div>
        </div>
        <div class="contact-item reveal reveal-delay-3">
          <div class="contact-icon"><i class="fa-solid fa-envelope"></i></div>
          <div class="contact-item-text">
            <strong>Email</strong>
            <span>Kwakudovlo84@icloud.com</span>
          </div>
        </div>
        <div class="contact-item reveal reveal-delay-4">
          <div class="contact-icon"><i class="fa-regular fa-clock"></i></div>
          <div class="contact-item-text">
            <strong>Hours</strong>
            <span>Tus – Fri: 8AM – 10PM &nbsp;|&nbsp; Sat 9AM – 10PM | Sun: 1AM – 10PM</span>
          </div>
        </div>
      </div>
       <div class="social-links reveal">
        <a href="#" class="social-link"><i class="fa-brands fa-instagram"></i></a>
        <a href="#" class="social-link"><i class="fa-brands fa-tiktok"></i></a>
        <a href="#" class="social-link"><i class="fa-brands fa-x-twitter"></i></a>
        <a href="#" class="social-link"><i class="fa-brands fa-facebook-f"></i></a>
        <a href="#" class="social-link"><i class="fa-brands fa-whatsapp"></i></a>
        <a href="#" class="social-link"><i class="fa-brands fa-snapchat"></i></a>
      </div>
    </div>
   <div style="display:flex;flex-direction:column;gap:0.8rem;" class="reveal reveal-delay-2">
      <div class="map-container">
        <iframe
          id="shopMap"
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d250!2d0.05003!3d5.75723!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zNcKwNDUnMjYuMCJOIDDCsDAzJzAwLjEiRQ!5e0!3m2!1sen!2sgh!4v1700000000000!5m2!1sen!2sgh"
          allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade">
        </iframe>
      </div>
      <button id="resetMapBtn" onclick="resetMapLocation()" style="
        display:inline-flex;align-items:center;justify-content:center;gap:10px;
        width:100%;padding:13px 20px;
        background:transparent;
        border:1px solid var(--border);
        border-radius:8px;
        color:var(--gold);
        font-family:'Outfit',sans-serif;
        font-size:0.78rem;letter-spacing:0.2em;
        text-transform:uppercase;font-weight:500;
        cursor:pointer;
        transition:background 0.3s,border-color 0.3s,transform 0.3s,box-shadow 0.3s;
      "
      onmouseover="this.style.background='rgba(201,168,76,0.1)';this.style.borderColor='var(--gold)';this.style.transform='translateY(-2px)';this.style.boxShadow='0 6px 20px rgba(201,168,76,0.15)'"
      onmouseout="this.style.background='transparent';this.style.borderColor='rgba(201,168,76,0.18)';this.style.transform='translateY(0)';this.style.boxShadow='none'"
      >
        <i class="fa-solid fa-location-dot"></i> Shop Location
      </button>
    </div>
  </div>
</section>

<!-- ─── FOOTER ─── -->
<footer>
  <div class="footer-brand">OGEE'S <span>STYLISH CUT</span></div>
  <p class="footer-copy">© 2026 Ogee's Stylish Cut. All rights reserved.</p>
  <div class="footer-links">
    <a href="#services">Services</a>
    <a href="#booking">Book</a>
    <a href="#contact">Contact</a>
  </div>
</footer>

<script>
  // ─── LOADER ───
  window.addEventListener('load', () => {
    setTimeout(() => {
      document.getElementById('loader').classList.add('hide');
    }, 2200);
  });

  // ─── CURSOR ───
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });
  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();
  document.querySelectorAll('a, button, .service-card, .team-card, .gallery-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '18px'; cursor.style.height = '18px';
      ring.style.width = '54px'; ring.style.height = '54px';
      ring.style.opacity = '0.4';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '10px'; cursor.style.height = '10px';
      ring.style.width = '36px'; ring.style.height = '36px';
      ring.style.opacity = '0.6';
    });
  });

  // ─── NAVBAR SCROLL ───
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // ─── MOBILE MENU ───
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobileMenu');
  hamburger.addEventListener('click', () => {
    mobileMenu.classList.toggle('open');
  });
  function closeMobile() {
    mobileMenu.classList.remove('open');
  }

  // ─── SCROLL REVEAL ───
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(el => observer.observe(el));

  // ─── BOOKING ───
  function handleBooking() {
    const name = document.querySelector('input[placeholder="Kwame"]').value;
    if (!name.trim()) {
      alert('Please enter your first name to book.');
      return;
    }
    const btn = document.querySelector('.form-submit');
    btn.textContent = '✓ Appointment Confirmed!';
    btn.style.background = '#2a7a4b';
    btn.style.color = '#fff';
    setTimeout(() => {
      btn.innerHTML = 'Confirm Appointment <i class="fa-solid fa-arrow-right" style="margin-left:8px"></i>';
      btn.style.background = '';
      btn.style.color = '';
    }, 3000);
  }
</script>
</body>
</html>
