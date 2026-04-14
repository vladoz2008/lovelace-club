# 🚀 Инструкция по настройке и запуску

## Шаг 1: Подготовка файлов

1. **Добавьте логотип**
   - Переименуйте файл `!Лавлейс.jpg` в `logo.jpg`
   - Поместите его в корневую директорию проекта
   - Убедитесь, что размер изображения оптимизирован (рекомендуется 500x500px)

## Шаг 2: Проверка локально

1. Откройте `index.html` в браузере
2. Проверьте, что:
   - ✅ Логотип отображается в навигации
   - ✅ Все секции загружаются корректно
   - ✅ Анимации работают при скролле
   - ✅ Мобильное меню открывается/закрывается
   - ✅ Форма обратной связи реагирует на отправку

## Шаг 3: Настройка контактов

Откройте `index.html` и замените:

```html
<!-- Строка 342-343 -->
<a href="https://t.me/ittopclub" class="contact-link" target="_blank">
    <span>Telegram: @ittopclub</span>
</a>
<a href="mailto:partners@ittopclub.ru" class="contact-link">
    <span>Email: partners@ittopclub.ru</span>
</a>
```

На ваши реальные контакты.

## Шаг 4: Публикация на GitHub Pages

### 4.1 Создание репозитория

1. Перейдите на [GitHub](https://github.com)
2. Нажмите "New repository"
3. Назовите репозиторий (например, `lovelace-club`)
4. Выберите "Public"
5. НЕ добавляйте README, .gitignore (они уже есть)
6. Нажмите "Create repository"

### 4.2 Загрузка файлов

Откройте терминал в папке проекта и выполните:

```bash
# Инициализация Git
git init

# Добавление всех файлов
git add .

# Первый коммит
git commit -m "Initial commit: Lovelace Club landing page"

# Переименование ветки в main
git branch -M main

# Добавление удаленного репозитория (замените YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/lovelace-club.git

# Отправка на GitHub
git push -u origin main
```

### 4.3 Активация GitHub Pages

1. Перейдите в ваш репозиторий на GitHub
2. Откройте **Settings** (⚙️)
3. В левом меню выберите **Pages**
4. В разделе **Source**:
   - Branch: `main`
   - Folder: `/ (root)`
5. Нажмите **Save**
6. Подождите 1-2 минуты

Ваш сайт будет доступен по адресу:
```
https://YOUR_USERNAME.github.io/lovelace-club/
```

## Шаг 5: Настройка формы обратной связи

### Вариант A: Telegram Bot (рекомендуется)

1. Создайте бота через [@BotFather](https://t.me/BotFather)
2. Получите токен бота
3. Узнайте ваш Chat ID через [@userinfobot](https://t.me/userinfobot)
4. Откройте `script.js` и замените код формы:

```javascript
contactForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    
    const formData = new FormData(contactForm);
    const name = formData.get('name') || contactForm.querySelector('input[type="text"]').value;
    const email = formData.get('email') || contactForm.querySelector('input[type="email"]').value;
    const role = formData.get('role') || contactForm.querySelector('select').value;
    const message = formData.get('message') || contactForm.querySelector('textarea').value;
    
    const telegramMessage = `
🆕 Новая заявка с сайта Лавлейс

👤 Имя: ${name}
📧 Email: ${email}
🎯 Роль: ${role}
💬 Сообщение: ${message || 'Не указано'}
    `.trim();
    
    const BOT_TOKEN = 'YOUR_BOT_TOKEN';
    const CHAT_ID = 'YOUR_CHAT_ID';
    
    try {
        const response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                chat_id: CHAT_ID,
                text: telegramMessage,
                parse_mode: 'HTML'
            })
        });
        
        if (response.ok) {
            alert('✅ Спасибо за заявку! Мы свяжемся с вами в ближайшее время.');
            contactForm.reset();
        } else {
            throw new Error('Ошибка отправки');
        }
    } catch (error) {
        alert('❌ Произошла ошибка. Попробуйте связаться с нами напрямую через Telegram.');
        console.error(error);
    }
});
```

### Вариант B: Google Forms

1. Создайте Google Form
2. Добавьте поля: Имя, Email, Роль, Сообщение
3. Получите ссылку для встраивания
4. Замените форму в `index.html` на iframe Google Forms

### Вариант C: EmailJS

1. Зарегистрируйтесь на [EmailJS](https://www.emailjs.com/)
2. Создайте email service
3. Создайте email template
4. Добавьте SDK в `index.html`:

```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
```

5. Инициализируйте в `script.js`:

```javascript
emailjs.init('YOUR_PUBLIC_KEY');

contactForm.addEventListener('submit', (e) => {
    e.preventDefault();
    
    emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', contactForm)
        .then(() => {
            alert('✅ Спасибо за заявку!');
            contactForm.reset();
        })
        .catch((error) => {
            alert('❌ Ошибка отправки');
            console.error(error);
        });
});
```

## Шаг 6: Оптимизация

### Сжатие изображений

Оптимизируйте `logo.jpg`:
- Используйте [TinyPNG](https://tinypng.com/)
- Или [Squoosh](https://squoosh.app/)
- Рекомендуемый размер: 500x500px, качество 80-85%

### Проверка производительности

1. Откройте сайт в Chrome
2. Нажмите F12 → Lighthouse
3. Запустите аудит
4. Исправьте найденные проблемы

## Шаг 7: Кастомизация

### Изменение цветов

Откройте `style.css` и измените переменные в `:root`:

```css
:root {
    --color-bg: #F5EFE7;        /* Фон */
    --color-primary: #213547;    /* Основной */
    --color-secondary: #4A90A4;  /* Вторичный */
    --color-accent: #7EBDC3;     /* Акцент */
}
```

### Изменение текста

Все тексты находятся в `index.html`. Просто найдите нужную секцию и отредактируйте.

### Добавление секций

Скопируйте структуру существующей секции и адаптируйте под свои нужды.

## 🆘 Решение проблем

### Логотип не отображается
- Проверьте, что файл называется `logo.jpg`
- Проверьте путь в `index.html`: `<img src="logo.jpg">`
- Убедитесь, что файл загружен в репозиторий

### Анимации не работают
- Проверьте подключение AOS.js в `index.html`
- Откройте консоль браузера (F12) и проверьте ошибки

### Форма не отправляется
- Проверьте настройки в `script.js`
- Убедитесь, что токены/ключи указаны правильно
- Проверьте консоль браузера на ошибки

### GitHub Pages не работает
- Подождите 5-10 минут после активации
- Проверьте, что репозиторий публичный (Public)
- Убедитесь, что в Settings → Pages выбрана ветка `main`

## 📞 Поддержка

Если возникли вопросы:
1. Проверьте [Issues](https://github.com/YOUR_USERNAME/lovelace-club/issues)
2. Создайте новый Issue с описанием проблемы
3. Напишите в Telegram: @ittopclub

---

**Удачи с запуском! 🚀**
