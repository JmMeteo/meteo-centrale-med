const LAT = 43.341000;
const LON = 5.438472;
const NAME = "Centrale Méditerranée";
const TZ = "Europe/Paris";

const WEATHER_CURRENT_FIELDS = [
  "temperature_2m",
  "apparent_temperature",
  "relative_humidity_2m",
  "pressure_msl",
  "wind_speed_10m",
  "wind_direction_10m",
  "wind_gusts_10m",
  "precipitation",
  "cloud_cover",
  "visibility",
  "uv_index",
  "shortwave_radiation",
  "direct_radiation",
  "diffuse_radiation",
  "weather_code",
  "is_day"
].join(",");

const WEATHER_HOURLY_FIELDS = [
  "temperature_2m",
  "precipitation_probability",
  "precipitation",
  "weather_code",
  "cloud_cover",
  "wind_speed_10m",
  "uv_index",
  "relative_humidity_2m"
].join(",");

const WEATHER_DAILY_FIELDS = [
  "weather_code",
  "temperature_2m_max",
  "temperature_2m_min",
  "sunrise",
  "sunset",
  "precipitation_probability_max",
  "wind_speed_10m_max"
].join(",");

const AIR_CURRENT_FIELDS = [
  "european_aqi",
  "pm2_5",
  "pm10",
  "nitrogen_dioxide",
  "ozone"
].join(",");

function toFloat(x, ndigits = 1) {
  const v = Number(x);
  return Number.isFinite(v) ? Number(v.toFixed(ndigits)) : null;
}

function toInt(x) {
  const v = Number(x);
  return Number.isFinite(v) ? Math.round(v) : null;
}

function safeGet(seq, idx, def = null) {
  try {
    return seq[idx];
  } catch {
    return def;
  }
}

function buildWeatherUrl() {
  const p = new URLSearchParams({
    latitude: LAT,
    longitude: LON,
    current: WEATHER_CURRENT_FIELDS,
    hourly: WEATHER_HOURLY_FIELDS,
    daily: WEATHER_DAILY_FIELDS,
    timezone: TZ,
    forecast_days: "7"
  });
  return `https://api.open-meteo.com/v1/forecast?${p.toString()}`;
}

function buildAirUrl() {
  const p = new URLSearchParams({
    latitude: LAT,
    longitude: LON,
    current: AIR_CURRENT_FIELDS,
    timezone: TZ,
    domains: "cams_europe"
  });
  return `https://air-quality-api.open-meteo.com/v1/air-quality?${p.toString()}`;
}

function aqiLabel(aqi) {
  if (aqi == null) return "—";
  if (aqi <= 20) return "Bonne";
  if (aqi <= 40) return "Correcte";
  if (aqi <= 60) return "Moyenne";
  if (aqi <= 80) return "Dégradée";
  if (aqi <= 100) return "Mauvaise";
  return "Très mauvaise";
}

function computeAdvice(cur, daily0, air) {
  const temp = cur.temp_c;
  const wind = cur.wind_kmh;
  const uv = cur.uv_index;
  const rain = cur.precip_mm;
  const cloud = cur.cloud_pct;
  const aqi = air.european_aqi;

  if (rain != null && rain >= 1.0) return "Pluie en cours, parapluie conseillé.";
  if (wind != null && wind >= 45) return "Vent soutenu, prudence à vélo ou à pied.";
  if (uv != null && uv >= 6) return "UV élevés, protection solaire conseillée.";
  if (temp != null && temp >= 30) return "Chaleur marquée, pense à bien t’hydrater.";
  if (aqi != null && aqi > 60) return "Qualité de l’air dégradée, limite l’effort intense dehors.";
  if (cloud != null && cloud <= 20) return "Temps bien dégagé, bonne luminosité.";
  if (daily0?.precip_prob_max != null && daily0.precip_prob_max >= 60) return "Risque de pluie plus tard, garde une veste.";
  return "Conditions globalement calmes en ce moment.";
}

function setText(id, v) {
  const el = document.getElementById(id);
  if (!el) return;
  el.textContent = (v === null || v === undefined || Number.isNaN(v)) ? "—" : v;
}

function apiStatusLabel(status) {
  if (status === "ok") return "OK";
  if (status === "error") return "Erreur";
  return "—";
}

function windDirToText(deg) {
  if (deg === null || deg === undefined || isNaN(deg)) return "—";
  const dirs = ["N","NNE","NE","ENE","E","ESE","SE","SSE","S","SSO","SO","OSO","O","ONO","NO","NNO"];
  const idx = Math.round(((deg % 360) / 22.5)) % 16;
  return dirs[idx];
}

function wmoToLabel(code) {
  const mapping = {
    0: "Ciel dégagé",
    1: "Peu nuageux",
    2: "Partiellement nuageux",
    3: "Couvert",
    45: "Brouillard",
    48: "Brouillard givrant",
    51: "Bruine légère",
    53: "Bruine modérée",
    55: "Bruine forte",
    56: "Bruine verglaçante légère",
    57: "Bruine verglaçante forte",
    61: "Pluie faible",
    63: "Pluie modérée",
    65: "Pluie forte",
    66: "Pluie verglaçante légère",
    67: "Pluie verglaçante forte",
    71: "Neige faible",
    73: "Neige modérée",
    75: "Neige forte",
    77: "Grains de neige",
    80: "Averses faibles",
    81: "Averses modérées",
    82: "Averses fortes",
    85: "Averses de neige faibles",
    86: "Averses de neige fortes",
    95: "Orage",
    96: "Orage avec grêle faible",
    99: "Orage avec grêle forte"
  };
  return mapping[code] || "Inconnu";
}

function weatherFamily(code) {
  if ([95,96,99].includes(code)) return "storm";
  if ([51,53,55,56,57,61,63,65,66,67,80,81,82].includes(code)) return "rain";
  if ([1,2,3,45,48].includes(code)) return "cloudy";
  return "clear";
}

function iconForCode(code, isDay) {
  const fam = weatherFamily(code);
  if (fam === "storm") return "⛈";
  if (fam === "rain") return "🌧";
  if ([45,48].includes(code)) return "🌫";
  if ([1,2,3].includes(code)) return isDay ? "⛅" : "☁";
  return isDay === 1 ? "☀" : "🌙";
}

function qualityPillClass(aqi) {
  if (aqi === null || aqi === undefined) return "warn";
  if (aqi <= 40) return "ok";
  if (aqi <= 80) return "warn";
  return "bad";
}

function setStatusPill(kind, txt) {
  const pill = document.getElementById("statusPill");
  pill.classList.remove("ok","warn","bad");
  pill.classList.add(kind);
  setText("statusTxt", txt);
}

function setAqiPill(aqi, label) {
  const pill = document.getElementById("aqiPill");
  pill.classList.remove("ok","warn","bad");
  pill.classList.add(qualityPillClass(aqi));
  setText("aqiTxt", "AQI " + (aqi ?? "—") + " • " + (label || "—"));
}

function formatHourLabel(s) {
  if (!s) return "—";
  const d = new Date(s);
  if (Number.isNaN(d.getTime())) return s;
  return d.toLocaleTimeString("fr-FR", {hour:"2-digit", minute:"2-digit"});
}

function formatDateLabel(s) {
  if (!s) return "—";
  const d = new Date(s);
  if (Number.isNaN(d.getTime())) return s;
  return d.toLocaleDateString("fr-FR", {weekday:"short", day:"2-digit", month:"2-digit"});
}

function phaseFromTimes(now, sunrise, sunset, isDay) {
  if (!sunrise || !sunset) return isDay === 1 ? "day" : "night";
  const sr = new Date(sunrise);
  const ss = new Date(sunset);
  if ([sr, ss].some(x => Number.isNaN(x.getTime()))) return isDay === 1 ? "day" : "night";

  const nowMs = now.getTime();
  const srMs = sr.getTime();
  const ssMs = ss.getTime();

  if (nowMs < srMs || nowMs > ssMs) return "night";
  if (nowMs >= srMs - 45 * 60000 && nowMs <= srMs + 90 * 60000) return "dawn";
  const noonMs = srMs + (ssMs - srMs) / 2;
  if (Math.abs(nowMs - noonMs) <= 90 * 60000) return "noon";
  if (nowMs >= ssMs - 120 * 60000) return "golden";
  return "day";
}

function applyTheme(code, isDay, cloudPct, sunrise, sunset) {
  document.body.classList.remove(
    "phase-dawn","phase-day","phase-noon","phase-golden","phase-night",
    "cloudy","rainy","stormy","night"
  );
  const fam = weatherFamily(code);
  const phase = phaseFromTimes(new Date(), sunrise, sunset, isDay);
  document.body.classList.add("phase-" + phase);

  if (fam === "cloudy" || fam === "rain" || fam === "storm" || (cloudPct ?? 0) >= 35) {
    document.body.classList.add("cloudy");
  }
  if (fam === "rain" || fam === "storm") {
    document.body.classList.add("rainy");
  }
  if (fam === "storm") {
    document.body.classList.add("stormy");
  }
  if (phase === "night") {
    document.body.classList.add("night");
  }
}

function renderDynamicClouds(cloudPct, isDay) {
  const layer = document.getElementById("cloudLayer");
  layer.innerHTML = "";
  const pct = Math.max(0, Math.min(100, Number(cloudPct || 0)));
  const count = Math.max(0, Math.round(pct / 14));

  for (let i = 0; i < count; i++) {
    const c = document.createElement("div");
    c.className = "cloud";
    const w = 160 + Math.random() * 240;
    const h = w * (0.28 + Math.random() * 0.14);
    c.style.width = w + "px";
    c.style.height = h + "px";
    c.style.top = (3 + Math.random() * 28) + "%";
    c.style.left = (-28 - Math.random() * 20) + "vw";
    let opacity = 0.04 + pct / 340 + Math.random() * 0.04;
    if (isDay === 0) opacity *= 0.9;
    c.style.opacity = opacity.toFixed(2);
    c.style.animationDuration = (42 + Math.random() * 52) + "s";
    c.style.animationDelay = (-Math.random() * 24) + "s";
    layer.appendChild(c);
  }
}

function seriesMin(values) {
  const valid = values.filter(v => v !== null && v !== undefined && !Number.isNaN(v)).map(Number);
  if (!valid.length) return null;
  return Math.min(...valid);
}

function seriesMax(values) {
  const valid = values.filter(v => v !== null && v !== undefined && !Number.isNaN(v)).map(Number);
  if (!valid.length) return null;
  return Math.max(...valid);
}

function polylineFromData(values, width, height, minPad = 10, maxPad = 10) {
  const nums = values.map(v => (v === null || v === undefined || isNaN(v)) ? null : Number(v));
  const valid = nums.filter(v => v !== null);
  if (!valid.length) return "";
  let vmin = Math.min(...valid);
  let vmax = Math.max(...valid);
  if (vmax === vmin) { vmax += 1; vmin -= 1; }
  return nums.map((v, i) => {
    const x = (i / (nums.length - 1)) * width;
    const y = height - ((v - vmin) / (vmax - vmin)) * (height - minPad - maxPad) - minPad;
    return (v === null) ? null : [x, y];
  }).filter(Boolean).map(p => p[0].toFixed(1) + "," + p[1].toFixed(1)).join(" ");
}

function barsFromData(values, width, height) {
  const nums = values.map(v => (v === null || v === undefined || isNaN(v)) ? 0 : Number(v));
  const vmax = Math.max(1, ...nums);
  const bw = width / nums.length;
  return nums.map((v, i) => {
    const bh = (v / vmax) * (height - 40);
    const x = i * bw + bw * 0.18;
    const y = height - bh - 18;
    const w = bw * 0.64;
    return `<rect x="${x.toFixed(1)}" y="${y.toFixed(1)}" width="${w.toFixed(1)}" height="${bh.toFixed(1)}" rx="3" fill="rgba(255,255,255,.20)"/>`;
  }).join("");
}

function areaFromData(values, width, height) {
  const nums = values.map(v => (v === null || v === undefined || isNaN(v)) ? 0 : Number(v));
  const vmax = Math.max(1, ...nums);
  const pts = nums.map((v, i) => {
    const x = (i / (nums.length - 1)) * width;
    const y = height - (v / vmax) * (height - 34) - 18;
    return `${x.toFixed(1)},${y.toFixed(1)}`;
  }).join(" ");
  return `0,${height-18} ${pts} ${width},${height-18}`;
}

function renderChartTempRain(hourly) {
  const box = document.getElementById("chartTempRain");
  const width = Math.max(260, box.clientWidth - 10);
  const height = 110;

  const temps = hourly.map(x => x.temp_c);
  const rain = hourly.map(x => x.precip_mm);
  const tempMin = seriesMin(temps);
  const tempMax = seriesMax(temps);
  const rainMax = seriesMax(rain);

  const tempLine = polylineFromData(temps, width, height, 24, 18);
  const rainBars = barsFromData(rain, width, height);

  box.innerHTML = `
  <svg width="100%" height="${height}" viewBox="0 0 ${width} ${height}" preserveAspectRatio="none">
    <text x="8" y="12" font-size="10" fill="rgba(255,255,255,.85)">Légende</text>
    <line x1="58" y1="9" x2="76" y2="9" stroke="rgba(255,255,255,.95)" stroke-width="2.5" />
    <text x="82" y="12" font-size="10" fill="rgba(255,255,255,.85)">Courbe : température</text>
    <rect x="182" y="4" width="14" height="8" rx="2" fill="rgba(255,255,255,.20)"/>
    <text x="201" y="12" font-size="10" fill="rgba(255,255,255,.85)">Barres : pluie</text>

    <text x="8" y="24" font-size="9" fill="rgba(255,255,255,.72)">Temp min ${tempMin ?? "—"}°C</text>
    <text x="${width-86}" y="24" font-size="9" fill="rgba(255,255,255,.72)">Temp max ${tempMax ?? "—"}°C</text>
    <text x="${width-86}" y="36" font-size="9" fill="rgba(255,255,255,.72)">Pluie max ${rainMax ?? "—"} mm</text>

    <line x1="0" y1="${height-18}" x2="${width}" y2="${height-18}" stroke="rgba(255,255,255,.10)" />
    ${rainBars}
    <polyline points="${tempLine}" fill="none" stroke="rgba(255,255,255,.95)" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>`;
}

function renderChartCloudWind(hourly) {
  const box = document.getElementById("chartCloudWind");
  const width = Math.max(260, box.clientWidth - 10);
  const height = 110;

  const clouds = hourly.map(x => x.cloud_pct);
  const winds = hourly.map(x => x.wind_kmh);
  const cloudMax = seriesMax(clouds);
  const windMin = seriesMin(winds);
  const windMax = seriesMax(winds);

  const cloudArea = areaFromData(clouds, width, height);
  const windLine = polylineFromData(winds, width, height, 24, 18);

  box.innerHTML = `
  <svg width="100%" height="${height}" viewBox="0 0 ${width} ${height}" preserveAspectRatio="none">
    <text x="8" y="12" font-size="10" fill="rgba(255,255,255,.85)">Légende</text>
    <rect x="58" y="4" width="14" height="8" rx="2" fill="rgba(255,255,255,.15)"/>
    <text x="77" y="12" font-size="10" fill="rgba(255,255,255,.85)">Zone : nuages</text>
    <line x1="150" y1="9" x2="168" y2="9" stroke="rgba(255,255,255,.92)" stroke-width="2.5" />
    <text x="174" y="12" font-size="10" fill="rgba(255,255,255,.85)">Courbe : vent</text>

    <text x="8" y="24" font-size="9" fill="rgba(255,255,255,.72)">Vent min ${windMin ?? "—"} km/h</text>
    <text x="${width-92}" y="24" font-size="9" fill="rgba(255,255,255,.72)">Vent max ${windMax ?? "—"} km/h</text>
    <text x="${width-92}" y="36" font-size="9" fill="rgba(255,255,255,.72)">Nuages max ${cloudMax ?? "—"} %</text>

    <line x1="0" y1="${height-18}" x2="${width}" y2="${height-18}" stroke="rgba(255,255,255,.10)" />
    <polygon points="${cloudArea}" fill="rgba(255,255,255,.14)"></polygon>
    <polyline points="${windLine}" fill="none" stroke="rgba(255,255,255,.92)" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>`;
}

function renderHourlyCards(hourly) {
  const holder = document.getElementById("hourlyCards");
  holder.innerHTML = "";
  const every2h = hourly.filter((_, i) => i % 2 === 0).slice(0, 12);

  every2h.forEach(h => {
    const div = document.createElement("div");
    div.className = "hour-card";
    const code = h.weather_code;

    div.innerHTML = `
      <div class="hour-time">${formatHourLabel(h.time)}</div>
      <div class="hour-temp">${iconForCode(code, 1)} ${h.temp_c ?? "—"}°</div>
      <div class="small">${wmoToLabel(code)}</div>
      <div class="small">Pluie ${h.precip_prob_pct ?? "—"} %</div>
      <div class="small">Vent ${h.wind_kmh ?? "—"} km/h</div>
    `;
    holder.appendChild(div);
  });
}

function renderDailyCards(days) {
  const holder = document.getElementById("dailyCards");
  holder.innerHTML = "";

  days.slice(0, 5).forEach((d, idx) => {
    const div = document.createElement("div");
    div.className = "day-card";

    div.innerHTML = `
      <div class="day-date">${idx === 0 ? "Aujourd’hui" : formatDateLabel(d.date)}</div>
      <div class="day-temp">${iconForCode(d.weather_code, 1)} ${d.tmax_c ?? "—"}°</div>
      <div class="small">Min ${d.tmin_c ?? "—"}°</div>
      <div class="small">${wmoToLabel(d.weather_code)}</div>
      <div class="small">Pluie ${d.precip_prob_max ?? "—"} %</div>
    `;
    holder.appendChild(div);
  });
}

function updateSunProgress(sunrise, sunset) {
  const fill = document.getElementById("sunfill");
  const marker = document.getElementById("sunmarker");
  const txt = document.getElementById("sunProgressTxt");

  if (!sunrise || !sunset) {
    fill.style.width = "0%";
    marker.style.left = "0%";
    txt.textContent = "—";
    return;
  }

  const now = new Date();
  const sr = new Date(sunrise);
  const ss = new Date(sunset);

  if ([sr, ss].some(x => Number.isNaN(x.getTime()))) {
    fill.style.width = "0%";
    marker.style.left = "0%";
    txt.textContent = "—";
    return;
  }

  const total = ss.getTime() - sr.getTime();
  let ratio = (now.getTime() - sr.getTime()) / total;
  ratio = Math.max(0, Math.min(1, ratio));
  const pct = Math.round(ratio * 100);

  fill.style.width = pct + "%";
  marker.style.left = pct + "%";

  if (now < sr) txt.textContent = "Avant lever";
  else if (now > ss) txt.textContent = "Après coucher";
  else txt.textContent = pct + " %";
}

function transformData(weather, air) {
  const c = weather.current || {};
  const h = weather.hourly || {};
  const d = weather.daily || {};
  const ac = air.current || {};

  const hourlyTime = h.time || [];
  const hourlyTemp = h.temperature_2m || [];
  const hourlyWcode = h.weather_code || [];
  const hourlyPrecipProb = h.precipitation_probability || [];
  const hourlyPrecip = h.precipitation || [];
  const hourlyCloud = h.cloud_cover || [];
  const hourlyWind = h.wind_speed_10m || [];
  const hourlyUv = h.uv_index || [];
  const hourlyRh = h.relative_humidity_2m || [];

  const dailyTime = d.time || [];
  const dailyWcode = d.weather_code || [];
  const dailyTmax = d.temperature_2m_max || [];
  const dailyTmin = d.temperature_2m_min || [];
  const dailySunrise = d.sunrise || [];
  const dailySunset = d.sunset || [];
  const dailyPpmax = d.precipitation_probability_max || [];
  const dailyWmax = d.wind_speed_10m_max || [];

  const hourlyCards = [];
  for (let i = 0; i < Math.min(24, hourlyTime.length); i++) {
    hourlyCards.push({
      time: safeGet(hourlyTime, i),
      temp_c: toFloat(safeGet(hourlyTemp, i)),
      weather_code: toInt(safeGet(hourlyWcode, i)),
      precip_prob_pct: toInt(safeGet(hourlyPrecipProb, i)),
      precip_mm: toFloat(safeGet(hourlyPrecip, i)),
      cloud_pct: toInt(safeGet(hourlyCloud, i)),
      wind_kmh: toFloat(safeGet(hourlyWind, i)),
      uv_index: toFloat(safeGet(hourlyUv, i)),
      rh_pct: toInt(safeGet(hourlyRh, i))
    });
  }

  const dailyCards = [];
  for (let i = 0; i < Math.min(5, dailyTime.length); i++) {
    dailyCards.push({
      date: safeGet(dailyTime, i),
      weather_code: toInt(safeGet(dailyWcode, i)),
      tmax_c: toFloat(safeGet(dailyTmax, i)),
      tmin_c: toFloat(safeGet(dailyTmin, i)),
      sunrise: safeGet(dailySunrise, i),
      sunset: safeGet(dailySunset, i),
      precip_prob_max: toInt(safeGet(dailyPpmax, i)),
      wind_max_kmh: toFloat(safeGet(dailyWmax, i))
    });
  }

  const current = {
    time_local: c.time,
    temp_c: toFloat(c.temperature_2m),
    apparent_temp_c: toFloat(c.apparent_temperature),
    rh_pct: toInt(c.relative_humidity_2m),
    pressure_hpa: toFloat(c.pressure_msl),
    wind_kmh: toFloat(c.wind_speed_10m),
    wind_gust_kmh: toFloat(c.wind_gusts_10m),
    wind_dir_deg: toInt(c.wind_direction_10m),
    precip_mm: toFloat(c.precipitation),
    cloud_pct: toInt(c.cloud_cover),
    visibility_m: toInt(c.visibility),
    uv_index: toFloat(c.uv_index),
    irradiance_sw_wm2: toFloat(c.shortwave_radiation),
    irradiance_direct_wm2: toFloat(c.direct_radiation),
    irradiance_diffuse_wm2: toFloat(c.diffuse_radiation),
    weather_code: toInt(c.weather_code),
    is_day: toInt(c.is_day)
  };

  const airCurrent = {
    european_aqi: toInt(ac.european_aqi),
    aqi_label: aqiLabel(toInt(ac.european_aqi)),
    pm2_5: toFloat(ac.pm2_5),
    pm10: toFloat(ac.pm10),
    no2: toFloat(ac.nitrogen_dioxide),
    o3: toFloat(ac.ozone)
  };

  const quickSlots = {
    now: hourlyCards[0] || {},
    plus3h: hourlyCards[3] || {},
    soir: hourlyCards[12] || {},
    demain: dailyCards[1] || {}
  };

  const advice = computeAdvice(current, dailyCards[0] || {}, airCurrent);

  return {
    source: "open-meteo",
    location: { name: NAME, lat: LAT, lon: LON },
    fetched_at: new Date().toISOString(),
    status: "ok",
    last_error: null,
    weather: {
      current,
      hourly_24h: hourlyCards,
      daily_5d: dailyCards,
      quick_slots: quickSlots,
      advice
    },
    air: airCurrent
  };
}

async function load() {
  try {
    const weatherResponse = await fetch(buildWeatherUrl(), { cache: "no-store" });
    const weather = await weatherResponse.json();

    const airResponse = await fetch(buildAirUrl(), { cache: "no-store" });
    const air = await airResponse.json();

    const d = transformData(weather, air);

    const loc = d.location?.name || "Station";
    document.title = "Bulletin météo – " + loc;
    setText("title", "Bulletin météo – " + loc);

    setText("src", d.source || "—");
    setText("apiStatus", apiStatusLabel(d.status));
    setText("lastError", d.last_error || "Aucune");
    setText("coords", (d.location?.lat ?? "—") + ", " + (d.location?.lon ?? "—"));

    const fetched = d.fetched_at ? new Date(d.fetched_at) : null;
    if (fetched && !Number.isNaN(fetched.getTime())) {
      setText("updated", fetched.toLocaleString("fr-FR"));
      setText("freshness", "0 min");
      setStatusPill("ok", "OK");
    } else {
      setText("updated", "—");
      setText("freshness", "—");
      setStatusPill("warn", "Initialisation");
    }

    const c = d.weather?.current || {};
    const hourly = d.weather?.hourly_24h || [];
    const days = d.weather?.daily_5d || [];
    const q = d.weather?.quick_slots || {};
    const airData = d.air || {};

    setText("timeLocal", c.time_local);
    setText("temp", c.temp_c);
    setText("appTemp", c.apparent_temp_c);
    setText("rh", c.rh_pct);
    setText("p", c.pressure_hpa);
    setText("wind", c.wind_kmh);
    setText("gust", c.wind_gust_kmh);
    setText("wdirDeg", c.wind_dir_deg);
    setText("wdirTxt", windDirToText(c.wind_dir_deg));
    setText("rain", c.precip_mm);
    setText("cloud", c.cloud_pct);
    setText("uv", c.uv_index);
    setText("sw", c.irradiance_sw_wm2);
    setText("dir", c.irradiance_direct_wm2);
    setText("dif", c.irradiance_diffuse_wm2);
    setText("wcode", c.weather_code);

    const viskm = (c.visibility_m === null || c.visibility_m === undefined) ? null : Math.round((c.visibility_m / 1000) * 10) / 10;
    setText("vis", viskm);

    const label = wmoToLabel(c.weather_code);
    setText("etat", label);
    setText("moodTxt", label);
    setText("isDayTxt", c.is_day === 1 ? "Jour" : "Nuit");

    const parts = [];
    if (c.temp_c !== null && c.temp_c !== undefined) parts.push(c.temp_c + "°C");
    parts.push(label.toLowerCase());
    if (c.wind_kmh !== null && c.wind_kmh !== undefined) parts.push("vent " + c.wind_kmh + " km/h");
    setText("summary", parts.join(" • "));

    const d0 = days[0] || {};
    setText("sunrise", d0.sunrise ? formatHourLabel(d0.sunrise) : "—");
    setText("sunset", d0.sunset ? formatHourLabel(d0.sunset) : "—");
    setText("tminToday", d0.tmin_c);
    setText("tmaxToday", d0.tmax_c);
    setText("ppmaxToday", d0.precip_prob_max);
    setText("wmaxToday", d0.wind_max_kmh);
    updateSunProgress(d0.sunrise, d0.sunset);

    setText("qNowLabel", q.now ? wmoToLabel(q.now.weather_code) : "—");
    setText("qNowTemp", q.now?.temp_c);
    setText("q3Label", q.plus3h ? wmoToLabel(q.plus3h.weather_code) : "—");
    setText("q3Temp", q.plus3h?.temp_c);
    setText("qEveningLabel", q.soir ? wmoToLabel(q.soir.weather_code) : "—");
    setText("qEveningTemp", q.soir?.temp_c);
    setText("qTomorrowLabel", q.demain ? wmoToLabel(q.demain.weather_code) : "—");
    setText("qTomorrowTemp", q.demain?.tmax_c);

    setText("advice", d.weather?.advice || "—");

    setText("aqi", airData.european_aqi);
    setText("aqiLabel", airData.aqi_label);
    setText("pm25", airData.pm2_5);
    setText("pm10", airData.pm10);
    setText("no2", airData.no2);
    setText("o3", airData.o3);
    setAqiPill(airData.european_aqi, airData.aqi_label);

    applyTheme(c.weather_code, c.is_day, c.cloud_pct, d0.sunrise, d0.sunset);
    renderDynamicClouds(c.cloud_pct, c.is_day);
    renderHourlyCards(hourly);
    renderDailyCards(days);
    renderChartTempRain(hourly);
    renderChartCloudWind(hourly);

  } catch (e) {
    setStatusPill("bad", "Erreur");
    setText("apiStatus", "Erreur");
    setText("lastError", String(e));
  }

  setText("clock", new Date().toLocaleString("fr-FR"));
}

load();
setInterval(load, 60000);

window.addEventListener("resize", () => {
  load();
});
