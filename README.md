# Лавлейс | Бизнес-клуб для IT-специалистов и стартапов

Одностраничный лендинг для бизнес-клуба "Лавлейс" (бывший IT Top Club).

## 🚀 Описание проекта

Лавлейс — это экосистема для роста IT-специалистов и стартапов в России. Мы устраняем разрыв между возможностями и доступом в российском IT через:

- Менторство и обмен экспертизой
- Прокачку дефицитных навыков (ИБ, DevOps, AI/ML)
- Прямой доступ к венчурным фондам
- Нетворкинг и партнёрства

## 📋 Структура проекта

```
.
├── index.html          # Основная HTML-страница
├── style.css           # Стили (CSS)
├── script.js           # JavaScript функционал
├── logo.jpg            # Логотип проекта
└── README.md           # Документация
```

## 🎨 Особенности дизайна

- **Цветовая палитра**: Бежевый фон (#F5EFE7), темно-синий (#213547), голубые акценты (#4A90A4, #7EBDC3)
- **Адаптивный дизайн**: Полностью responsive для всех устройств
- **Анимации**: Плавные переходы и эффекты при скролле (AOS.js)
- **Интерактивность**: Плавающие геометрические фигуры, параллакс-эффекты

## 🛠️ Технологии

- HTML5
- CSS3 (Flexbox, Grid, CSS Variables)
- Vanilla JavaScript
- [AOS (Animate On Scroll)](https://michalsnik.github.io/aos/)

## 📦 Установка и запуск

### Локальный запуск

1. Клонируйте репозиторий:
```bash
git clone https://github.com/ваш-username/lovelace-club.git
cd lovelace-club
```

2. Добавьте файл `logo.jpg` в корневую директорию

3. Откройте `index.html` в браузере или используйте локальный сервер:
```bash
# С помощью Python
python -m http.server 8000

# С помощью Node.js (npx)
npx serve

# С помощью VS Code Live Server
# Установите расширение Live Server и нажмите "Go Live"
```

### Развертывание на GitHub Pages

1. Создайте репозиторий на GitHub

2. Инициализируйте Git и загрузите файлы:
```bash
git init
git add .
git commit -m "Initial commit: Lovelace Club landing page"
git branch -M main
git remote add origin https://github.com/ваш-username/lovelace-club.git
git push -u origin main
```

3. Включите GitHub Pages:
   - Перейдите в Settings → Pages
   - В разделе "Source" выберите ветку `main` и папку `/ (root)`
   - Нажмите "Save"

4. Ваш сайт будет доступен по адресу:
   `https://ваш-username.github.io/lovelace-club/`

## 📝 Настройка контента

### Изменение контактной информации

В файле `index.html` найдите секцию `<section class="contact">` и обновите:

```html
<a href="https://t.me/ваш-telegram" class="contact-link" target="_blank">
    <span class="icon">📱</span>
    <span>Telegram: @ваш-telegram</span>
</a>
<a href="mailto:ваш-email@example.com" class="contact-link">
    <span class="icon">✉️</span>
    <span>Email: ваш-email@example.com</span>
</a>
```

### Настройка формы обратной связи

В файле `script.js` найдите обработчик формы и добавьте интеграцию:

**Вариант 1: Telegram Bot API**
```javascript
contactForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    const formData = new FormData(contactForm);
    
    const message = `
        Новая заявка с сайта Лавлейс:
        Имя: ${formData.get('name')}
        Email: ${formData.get('email')}
        Роль: ${formData.get('role')}
        Сообщение: ${formData.get('message')}
    `;
    
    await fetch(`https://api.telegram.org/bot${YOUR_BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            chat_id: YOUR_CHAT_ID,
            text: message
        })
    });
    
    alert('Спасибо за заявку!');
    contactForm.reset();
});
```

**Вариант 2: Google Forms**
Создайте Google Form и используйте его URL для отправки данных.

**Вариант 3: EmailJS**
Зарегистрируйтесь на [EmailJS](https://www.emailjs.com/) и используйте их API.

## 🎯 Секции лендинга

1. **Hero** - Главный экран с призывом к действию
2. **Problem** - Проблемы IT-рынка России (статистика)
3. **Solution** - Решение: что предлагает Лавлейс
4. **Formats** - Форматы мероприятий
5. **Roadmap** - Дорожная карта развития (5 лет)
6. **Partners** - Партнёры клуба
7. **Contact** - Контактная форма и информация

## 🎨 Кастомизация цветов

В файле `style.css` измените CSS-переменные:

```css
:root {
    --color-bg: #F5EFE7;           /* Основной фон */
    --color-primary: #213547;       /* Основной цвет */
    --color-secondary: #4A90A4;     /* Вторичный цвет */
    --color-accent: #7EBDC3;        /* Акцентный цвет */
    --color-peach: #F4A261;         /* Дополнительный акцент */
}
```

## 🐛 Известные особенности

- **Пасхалка**: Попробуйте ввести код Konami (↑↑↓↓←→←→BA) 😉
- **Параллакс**: Плавающие фигуры на hero-секции реагируют на скролл
- **Анимации**: Элементы появляются при прокрутке страницы

## 📱 Адаптивность

Лендинг полностью адаптирован для:
- Desktop (1200px+)
- Tablet (768px - 1199px)
- Mobile (до 767px)

## 🤝 Контакты

- **Telegram**: [@ittopclub](https://t.me/ittopclub)
- **Email**: partners@ittopclub.ru

## 📄 Лицензия

Этот проект создан для бизнес-клуба "Лавлейс". Все права защищены.

---

**Санкт-Петербург | 2026**

Сделано с ❤️ для IT-сообщества
