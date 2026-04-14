# 🔌 Интеграции для лендинга "Лавлейс"

## 📱 Telegram Bot (Рекомендуется)

### Преимущества
- ✅ Бесплатно
- ✅ Мгновенные уведомления
- ✅ Простая настройка
- ✅ Не требует backend

### Настройка

#### Шаг 1: Создание бота

1. Откройте [@BotFather](https://t.me/BotFather) в Telegram
2. Отправьте команду `/newbot`
3. Введите название бота: `Lovelace Club Bot`
4. Введите username: `lovelace_club_bot`
5. Скопируйте токен (выглядит как `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)

#### Шаг 2: Получение Chat ID

1. Откройте [@userinfobot](https://t.me/userinfobot)
2. Нажмите Start
3. Скопируйте ваш Chat ID (например, `123456789`)

#### Шаг 3: Интеграция в код

Откройте `script.js` и замените обработчик формы:

```javascript
// Telegram Bot Configuration
const TELEGRAM_BOT_TOKEN = 'YOUR_BOT_TOKEN_HERE';
const TELEGRAM_CHAT_ID = 'YOUR_CHAT_ID_HERE';

// Form submission handler
const contactForm = document.querySelector('.contact-form');

if (contactForm) {
    contactForm.addEventListener('submit', async (e) => {
        e.preventDefault();
        
        // Get form data
        const name = contactForm.querySelector('input[type="text"]').value;
        const email = contactForm.querySelector('input[type="email"]').value;
        const role = contactForm.querySelector('select').value;
        const message = contactForm.querySelector('textarea').value;
        
        // Format message
        const telegramMessage = `
🆕 <b>Новая заявка с сайта Лавлейс</b>

👤 <b>Имя:</b> ${name}
📧 <b>Email:</b> ${email}
🎯 <b>Роль:</b> ${getRoleText(role)}
💬 <b>Сообщение:</b> ${message || 'Не указано'}

⏰ <b>Время:</b> ${new Date().toLocaleString('ru-RU')}
        `.trim();
        
        // Send to Telegram
        try {
            const response = await fetch(`https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    chat_id: TELEGRAM_CHAT_ID,
                    text: telegramMessage,
                    parse_mode: 'HTML'
                })
            });
            
            if (response.ok) {
                // Success
                alert('✅ Спасибо за заявку! Мы свяжемся с вами в ближайшее время.');
                contactForm.reset();
            } else {
                throw new Error('Ошибка отправки');
            }
        } catch (error) {
            // Error
            console.error('Error:', error);
            alert('❌ Произошла ошибка при отправке. Пожалуйста, свяжитесь с нами напрямую через Telegram: @ittopclub');
        }
    });
}

// Helper function
function getRoleText(role) {
    const roles = {
        'specialist': 'IT-специалист',
        'startup': 'Стартап',
        'partner': 'Потенциальный партнёр'
    };
    return roles[role] || role;
}
```

---

## 📧 EmailJS

### Преимущества
- ✅ Отправка на email
- ✅ Бесплатный план (200 писем/месяц)
- ✅ Шаблоны писем
- ✅ Не требует backend

### Настройка

#### Шаг 1: Регистрация

1. Зарегистрируйтесь на [EmailJS](https://www.emailjs.com/)
2. Подтвердите email

#### Шаг 2: Настройка сервиса

1. Перейдите в Email Services
2. Добавьте сервис (Gmail / Outlook / и т.д.)
3. Скопируйте Service ID

#### Шаг 3: Создание шаблона

1. Перейдите в Email Templates
2. Create New Template
3. Используйте переменные:
   ```
   Новая заявка с сайта Лавлейс
   
   Имя: {{name}}
   Email: {{email}}
   Роль: {{role}}
   Сообщение: {{message}}
   ```
4. Скопируйте Template ID

#### Шаг 4: Интеграция

Добавьте в `index.html` перед закрывающим `</body>`:

```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
<script>
    emailjs.init('YOUR_PUBLIC_KEY');
</script>
```

Обновите `script.js`:

```javascript
const contactForm = document.querySelector('.contact-form');

if (contactForm) {
    contactForm.addEventListener('submit', (e) => {
        e.preventDefault();
        
        // Get form data
        const templateParams = {
            name: contactForm.querySelector('input[type="text"]').value,
            email: contactForm.querySelector('input[type="email"]').value,
            role: contactForm.querySelector('select').value,
            message: contactForm.querySelector('textarea').value
        };
        
        // Send email
        emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams)
            .then(() => {
                alert('✅ Спасибо за заявку!');
                contactForm.reset();
            })
            .catch((error) => {
                console.error('Error:', error);
                alert('❌ Ошибка отправки');
            });
    });
}
```

---

## 📊 Google Analytics

### Настройка

#### Шаг 1: Создание аккаунта

1. Перейдите на [Google Analytics](https://analytics.google.com/)
2. Создайте аккаунт и ресурс
3. Скопируйте Measurement ID (G-XXXXXXXXXX)

#### Шаг 2: Интеграция

Добавьте в `<head>` файла `index.html`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

#### Шаг 3: Отслеживание событий

Добавьте в `script.js`:

```javascript
// Track button clicks
document.querySelectorAll('.btn-primary').forEach(btn => {
    btn.addEventListener('click', () => {
        gtag('event', 'click', {
            'event_category': 'CTA',
            'event_label': btn.textContent
        });
    });
});

// Track form submission
contactForm.addEventListener('submit', () => {
    gtag('event', 'submit', {
        'event_category': 'Form',
        'event_label': 'Contact Form'
    });
});
```

---

## 📈 Yandex.Metrika

### Настройка

#### Шаг 1: Создание счётчика

1. Перейдите на [Yandex.Metrika](https://metrika.yandex.ru/)
2. Добавьте новый счётчик
3. Скопируйте код счётчика

#### Шаг 2: Интеграция

Добавьте перед закрывающим `</body>` в `index.html`:

```html
<!-- Yandex.Metrika counter -->
<script type="text/javascript" >
   (function(m,e,t,r,i,k,a){m[i]=m[i]||function(){(m[i].a=m[i].a||[]).push(arguments)};
   m[i].l=1*new Date();
   for (var j = 0; j < document.scripts.length; j++) {if (document.scripts[j].src === r) { return; }}
   k=e.createElement(t),a=e.getElementsByTagName(t)[0],k.async=1,k.src=r,a.parentNode.insertBefore(k,a)})
   (window, document, "script", "https://mc.yandex.ru/metrika/tag.js", "ym");

   ym(XXXXXXXX, "init", {
        clickmap:true,
        trackLinks:true,
        accurateTrackBounce:true,
        webvisor:true
   });
</script>
<noscript><div><img src="https://mc.yandex.ru/watch/XXXXXXXX" style="position:absolute; left:-9999px;" alt="" /></div></noscript>
<!-- /Yandex.Metrika counter -->
```

---

## 💬 Telegram Widget

### Интеграция чата

Добавьте перед закрывающим `</body>`:

```html
<!-- Telegram Widget -->
<script async src="https://telegram.org/js/telegram-widget.js?22" 
        data-telegram-login="lovelace_club_bot" 
        data-size="large" 
        data-radius="10" 
        data-auth-url="https://your-site.com/auth" 
        data-request-access="write">
</script>
```

Или кнопка "Написать в Telegram":

```html
<a href="https://t.me/ittopclub" target="_blank" class="telegram-button">
    <svg><!-- Telegram icon --></svg>
    Написать в Telegram
</a>
```

---

## 🎨 Дополнительные интеграции

### Favicon

Создайте favicon и добавьте в `<head>`:

```html
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
```

### Open Graph (для соцсетей)

Добавьте в `<head>`:

```html
<!-- Open Graph -->
<meta property="og:title" content="Лавлейс | Бизнес-клуб для IT-специалистов">
<meta property="og:description" content="Экосистема для роста IT-специалистов и стартапов">
<meta property="og:image" content="https://your-site.com/og-image.jpg">
<meta property="og:url" content="https://your-site.com">
<meta property="og:type" content="website">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Лавлейс | Бизнес-клуб для IT-специалистов">
<meta name="twitter:description" content="Экосистема для роста IT-специалистов и стартапов">
<meta name="twitter:image" content="https://your-site.com/twitter-image.jpg">
```

### Google Fonts (опционально)

Если хотите использовать кастомные шрифты:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

И обновите в `style.css`:

```css
:root {
    --font-primary: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

---

## 🔒 Безопасность

### Content Security Policy

Добавьте в `<head>`:

```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; 
               script-src 'self' 'unsafe-inline' https://unpkg.com https://api.telegram.org; 
               style-src 'self' 'unsafe-inline' https://unpkg.com; 
               img-src 'self' data: https:;">
```

### Rate Limiting для Telegram Bot

Добавьте в `script.js`:

```javascript
let lastSubmitTime = 0;
const SUBMIT_COOLDOWN = 60000; // 1 минута

contactForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    
    const now = Date.now();
    if (now - lastSubmitTime < SUBMIT_COOLDOWN) {
        alert('⏳ Пожалуйста, подождите минуту перед следующей отправкой');
        return;
    }
    
    // ... rest of the code
    
    lastSubmitTime = now;
});
```

---

## 📞 Поддержка

Если возникли вопросы по интеграциям:
- Telegram: @ittopclub
- Email: partners@ittopclub.ru

---

**Удачи с настройкой! 🚀**
