# Flask Vue Books

## 1.Server
flask + flask-sqlalchemy + flask-cors

### 1.1 Install and Environment
``` bash
conda install mamba
mamba create -n flask flask
conda activate flask

mamba install flask-sqlalchemy
mamba install flask-cors
mamba list

pip install pipreqs
pipreq ./ # Generate requirements.txt
```

### 1.2 Flask run-time
``` bash
flask --help # Get flask cli commands with help
flask routes # Get app.py routes current

# Start flask app on http://127.0.0.1:5000/
python app.py
```

### 1.3 Flask API for Books
``` http
GET http://127.0.0.1:5000/books/
Accept: application/json

POST http://127.0.0.1:5000/books
Content-Type: application/json
{ }

PUT http://127.0.0.1:5000/books/4
Content-Type: application/json
{ }

DELETE http://127.0.0.1:5000/books/5
Accept: application/json
```

## 2. User Interface
vite + vue3 + element-plus + axios

### 2.1 Install and Environment
``` bash
npm init vite@latest
# cd project-name
npm install
npm run dev

npm install --save element-plus
npm install --save axios
```

### 2.2 Nodejs run-time
``` bash
npm run dev # "dev": "vite",
npm run build # "build": "vite build",
npm run preview # "preview": "vite preview"
```