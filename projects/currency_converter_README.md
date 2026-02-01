<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Fira+Code&size=28&duration=2800&pause=2000&color=646CFF&center=true&vCenter=true&width=600&height=70&lines=Currency+Converter;React+%2B+Vite" alt="Typing SVG" />
</p>

<div align="center">

![React](https://img.shields.io/badge/React-18.3.1-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Vite](https://img.shields.io/badge/Vite-Latest-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

A modern, real-time **Currency Converter** web application built with **React 18.3.1** and **Vite**. Features instant conversion between multiple currencies with live exchange rates.

### Key Features

- 💱 **Real-time Conversion** with live exchange rates
- 🌍 **30+ Currencies** supported
- ⚡ **Instant Updates** as you type
- 🎨 **Modern UI** with smooth animations
- 📱 **Fully Responsive** design
- 🔄 **Historical Rates** support
- 💾 **Recent Conversions** history

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| **Framework** | React 18.3.1 |
| **Build Tool** | Vite |
| **Language** | JavaScript (ES6+) |
| **API** | ExchangeRate-API |
| **Styling** | CSS3 Modules |
| **Deployment** | Ready for Vercel/Netlify |

---

## 📦 Installation

### Prerequisites

- Node.js 16+ and npm/yarn/pnpm

### Step 1: Clone the Repository

```bash
git clone https://github.com/melxiory/currency_converter.git
cd currency_converter
```

### Step 2: Install Dependencies

```bash
npm install
# or
yarn install
# or
pnpm install
```

### Step 3: Run Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Visit `http://localhost:5173` in your browser.

### Step 4: Build for Production

```bash
npm run build
# or
yarn build
# or
pnpm build
```

---

## 📁 Project Structure

```
currency_converter/
├── src/
│   ├── components/         # React components
│   │   ├── Converter.jsx   # Main converter component
│   │   ├── CurrencySelect.jsx
│   │   └── ResultDisplay.jsx
│   ├── hooks/              # Custom hooks
│   │   └── useCurrency.js  # Currency API hook
│   ├── utils/              # Helper functions
│   ├── App.jsx             # Root component
│   ├── App.css             # Global styles
│   └── main.jsx            # Entry point
├── public/                 # Static assets
├── index.html
├── vite.config.js
└── package.json
```

---

## 🎯 Features Explained

### Real-time Conversion

The converter fetches live exchange rates and updates instantly:

```javascript
const [amount, setAmount] = useState(1);
const [fromCurrency, setFromCurrency] = useState('USD');
const [toCurrency, setToCurrency] = useState('EUR');
const [result, setResult] = useState(null);

useEffect(() => {
  const convert = async () => {
    const rate = await getExchangeRate(fromCurrency, toCurrency);
    setResult(amount * rate);
  };
  convert();
}, [amount, fromCurrency, toCurrency]);
```

### Supported Currencies

- 🇺🇸 USD - US Dollar
- 🇪🇺 EUR - Euro
- 🇬🇧 GBP - British Pound
- 🇯🇵 JPY - Japanese Yen
- 🇨🇭 CHF - Swiss Franc
- 🇨🇦 CAD - Canadian Dollar
- 🇦🇺 AUD - Australian Dollar
- 🇨🇳 CNY - Chinese Yuan
- 🇷🇺 RUB - Russian Ruble
- And 20+ more...

---

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
VITE_API_KEY=your_api_key_here
VITE_API_BASE_URL=https://api.exchangerate-api.com/v4
```

### API Integration

The app uses [ExchangeRate-API](https://www.exchangerate-api.com/) for live rates. Get your free API key [here](https://app.exchangerate-api.com/sign-up).

---

## 📸 Screenshots

<!-- Add your screenshots here -->
<p align="center">
  <img src="screenshots/converter.png" alt="Currency Converter" width="800">
</p>

---

## 🎨 Customization

### Theme Colors

Update colors in `App.css`:

```css
:root {
  --primary-color: #646CFF;
  --secondary-color: #61DAFB;
  --background: #ffffff;
  --text-color: #213547;
}
```

### Add More Currencies

Edit `src/utils/currencies.js`:

```javascript
export const currencies = [
  { code: 'USD', name: 'US Dollar', symbol: '$', flag: '🇺🇸' },
  { code: 'EUR', name: 'Euro', symbol: '€', flag: '🇪🇺' },
  // Add more currencies here
];
```

---

## 🚀 Deployment

### Vercel

```bash
npm install -g vercel
vercel
```

### Netlify

```bash
npm run build
# Deploy the 'dist' folder
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**melxiory**

- GitHub: [@melxiory](https://github.com/melxiory)

---

## 🙏 Acknowledgments

- [React](https://react.dev/) - The library for web and native user interfaces
- [Vite](https://vitejs.dev/) - Next Generation Frontend Tooling
- [ExchangeRate-API](https://www.exchangerate-api.com/) - Free currency exchange rates

---

<div align="center">

### 🌟 Star this repo if it helped you!

[![GitHub stars](https://img.shields.io/github/stars/melxiory/currency_converter?style=social)](https://github.com/melxiory/currency_converter/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/melxiory/currency_converter?style=social)](https://github.com/melxiory/currency_converter/network/members)

### 🎮 Try it online

[![Demo](https://img.shields.io/badge/Demo-Live-646CFF?style=for-the-badge&logo=vercel)](https://currency-converter-demo.vercel.app/)

</div>
