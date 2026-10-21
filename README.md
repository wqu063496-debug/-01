
<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#090d2b">
<title>575でチトセ愛</title>
<style>
:root {
  --ink: #f7f2ff;
  --muted: #c5c6ed;
  --pink: #ffb8e7;
  --gold: #ffe8a3;
  --glass: rgba(18,22,66,.72);
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 22px;
  color: var(--ink);
  font-family: "Hiragino Mincho ProN", "Yu Mincho", serif;
  background:
    radial-gradient(ellipse at 18% 18%, rgba(111,91,190,.45), transparent 35%),
    radial-gradient(ellipse at 85% 72%, rgba(99,53,146,.35), transparent 36%),
    linear-gradient(145deg, #06091e, #111943 55%, #24133d);
  overflow-x: hidden;
  position: relative;
}

main {
  width: min(720px, 100%);
  position: relative;
  z-index: 1;
  border: 1px solid rgba(202,196,255,.45);
  border-radius: 24px;
  padding: clamp(24px,6vw,52px);
  background: linear-gradient(
    145deg,
    rgba(24,30,83,.86),
    rgba(24,14,57,.82)
  );
  box-shadow: 0 0 45px rgba(130,112,255,.16);
  backdrop-filter: blur(8px);
}

h1 {
  text-align: center;
  font-size: clamp(30px,7vw,49px);
  letter-spacing: .12em;
  margin: 10px 0 12px;
  color: #fff5ff;
  text-shadow: 0 0 18px rgba(255,184,231,.45);
}

.intro {
  text-align: center;
  color: var(--muted);
  margin: 0 0 30px;
  font-size: 14px;
  line-height: 1.8;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 9px;
  color: #f0ddff;
  font-size: 14px;
}

input {
  width: 100%;
  padding: 14px 15px;
  border: 1px solid rgba(206,198,255,.5);
  border-radius: 12px;
  background: rgba(5,9,35,.65);
  color: white;
  font: inherit;
  font-size: 16px;
  outline: none;
}

input:focus {
  border-color: var(--pink);
  box-shadow: 0 0 0 3px rgba(255,184,231,.13);
}

input::placeholder {
  color: #a6a8d0;
}

button {
  margin-top: 16px;
  width: 100%;
  padding: 16px 12px;
  border: 1px solid rgba(255,255,255,.35);
  border-radius: 13px;
  background: linear-gradient(
    100deg, #7068d8, #b56bb8 58%, #e58abf
  );
  color: white;
  font: inherit;
  font-weight: bold;
  font-size: 16px;
  letter-spacing: .07em;
  cursor: pointer;
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
  box-shadow: 0 7px 22px rgba(116,86,209,.25);
  transition: transform .12s, filter .12s;
}

button:hover {
  filter: brightness(1.12);
}

button:active {
  transform: scale(.985);
}

button:focus-visible {
  outline: 3px solid var(--gold);
  outline-offset: 3px;
}

.result {
  margin-top: 27px;
  padding: 25px 16px 22px;
  min-height: 220px;
  border: 1px solid rgba(207,196,255,.3);
  border-radius: 18px;
  background: rgba(6,10,37,.42);
  display: none;
}

.result.show {
  display: block;
  animation: appear .4s ease-out;
}

.haiku {
  white-space: pre-line;
  text-align: center;
  font-size: clamp(23px,5vw,34px);
  line-height: 1.9;
  letter-spacing: .12em;
  color: #fff8ff;
}

.author {
  text-align: center;
  margin: 10px 0 0;
  color: var(--gold);
  font-size: 14px;
  letter-spacing: .1em;
}

.extra {
  margin: 23px auto 0;
  max-width: 100%;
  width: fit-content;
  color: var(--pink);
  font-family: "Hiragino Kaku Gothic ProN", "Yu Gothic", sans-serif;
  font-weight: 900;
  font-size: clamp(17px,4vw,24px);
  line-height: 1.6;
  text-align: center;
  transform: rotate(-2deg);
  overflow-wrap: anywhere;
}

.note {
  text-align: center;
  font-size: 11px;
  color: #a6a9d6;
  margin: 20px 0 0;
  line-height: 1.7;
}

.starline {
  text-align: center;
  color: #d8c9ff;
  letter-spacing: .6em;
  margin-top: 20px;
  opacity: .8;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(9px) scale(.99);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes twinkle {
  from { opacity: .55; }
  to { opacity: 1; }
}

@media (prefers-reduced-motion: reduce) {
  *, *:before, *:after {
    animation: none !important;
    transition: none !important;
  }
}
</style>
</head>
<body>
<main>
  <h1>575でチトセ愛</h1>
  <p class="intro">
    星空の下で名句をひとつ。<br>
    そして今日も、チトセへの愛は字余り。
  </p>

  <label for="authorName">
    俳句を書いた人の名前（署名）
  </label>
  <input
    id="authorName"
    value=""
    maxlength="30"
    placeholder="あなたの名前を入力"
    autocomplete="name"
    enterkeyhint="go"
  >

  <button id="draw" type="button">
    ✦　一句、そして愛を抽出する　✦
  </button>

  <section class="result" id="result"
    aria-live="polite" aria-atomic="true">
    <div class="haiku" id="haiku"></div>
    <div class="author" id="author"></div>
    <div class="extra" id="extra"></div>
  </section>

  <div class="starline" aria-hidden="true">
    ✧ · ˚　✦　˚ · ✧
  </div>

  <p class="note">
    ※俳句は有名な句からランダムに選ばれます。<br>
    チトセ愛の字余りは仕様です。
  </p>
</main>
</body>
</html>
