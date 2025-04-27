<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Netlify Form with Loading and Success</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
            text-align: center;
        }
        
        form {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-width: 400px;
            margin: 0 auto;
        }
        
        input,
        button {
            padding: 10px;
            font-size: 16px;
        }
        
        .message {
            display: none;
            margin-top: 20px;
            font-size: 18px;
        }
        
        .loading-message {
            color: orange;
        }
        
        .success-message {
            color: green;
        }
        
        .error-message {
            color: red;
        }
    </style>
</head>

<body>

    <h1>Send your data</h1>

    <form name="contact" netlify>
        <p>
            <label>Name <input type="text" name="name" /></label>
        </p>
        <p>
            <label>Email <input type="email" name="email" /></label>
        </p>
        <p>
            <button type="submit">Send</button>
        </p>
    </form>

    <div id="loading" class="message loading-message">⏳ جاري الإرسال...</div>
    <div id="success" class="message success-message">✅ تم إرسال البيانات بنجاح!</div>
    <div id="error" class="message error-message">❌ حصل خطأ، حاول مرة تانية.</div>

    <script>
        function handleSubmit(event) {
            event.preventDefault();
            const form = event.target;

            // نظهر رسالة جاري الإرسال
            document.getElementById('loading').style.display = 'block';
            form.style.display = 'none';

            const formData = new FormData(form);

            fetch('/', {
                method: 'POST',
                body: formData,
            }).then(() => {
                document.getElementById('loading').style.display = 'none';
                document.getElementById('success').style.display = 'block';
            }).catch((error) => {
                document.getElementById('loading').style.display = 'none';
                document.getElementById('error').style.display = 'block';
            });
        }
    </script>

</body>

</html>
