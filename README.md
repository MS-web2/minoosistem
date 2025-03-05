from flask import Flask, render_template_string, url_for

app = Flask(__name__)

@app.route('/')
def index():
    images = [
        {"filename": "image1.jpg", "price": "100,000 تومان"},
        {"filename": "image2.jpg", "price": "200,000 تومان"},
        {"filename": "image3.jpg", "price": "300,000 تومان"},
        {"filename": "image4.jpg", "price": "400,000 تومان"},
        {"filename": "image5.jpg", "price": "500,000 تومان"},
        {"filename": "image6.jpg", "price": "600,000 تومان"},
        {"filename": "image7.jpg", "price": "700,000 تومان"},
        {"filename": "image8.jpg", "price": "800,000 تومان"},
        {"filename": "image9.jpg", "price": "900,000 تومان"},
        {"filename": "image10.jpg", "price": "1,000,000 تومان"},
    ]

    html_code = """
    <!DOCTYPE html>
    <html lang="fa">
    <center>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>گالری تصاویر</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                text-align: center;
                direction: rtl;
            }
            .gallery {
                display: flex;
                flex-wrap: wrap;
                justify-content: center;
                gap: 15px;
                max-width: 900px;
                margin: auto;
            }
            .image-container {
                position: relative;
                width: 180px;
                height: 180px;
            }
            .image-container img {
                width: 100%;
                height: 100%;
                border-radius: 10px;
                transition: transform 0.3s ease;
            }
            .image-container:hover img {
                transform: scale(1.1);
            }
            .price-tag {
                position: absolute;
                bottom: 10px;
                left: 50%;
                transform: translateX(-50%);
                background: rgba(0, 0, 0, 0.7);
                color: white;
                padding: 5px 10px;
                border-radius: 5px;
                opacity: 0;
                transition: opacity 0.3s ease;
                font-size: 14px;
            }
            .image-container:hover .price-tag {
                opacity: 1;
            }
        </style>
    </center>
    </head>
    <body>
        <h1>گالری تصاویر</h1>
        <div class="gallery">
            {% for img in images %}
                <div class="image-container">
                    <img src="{{ url_for('static', filename=img.filename) }}" alt="تصویر">
                    <div class="price-tag">{{ img.price }}</div>
                </div>
            {% endfor %}
        </div>
    </body>
    </html>
    """
    return render_template_string(html_code, images=images)

if __name__ == '__main__':
    app.run(debug=True)
