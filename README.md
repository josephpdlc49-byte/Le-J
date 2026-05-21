

from Flask import Flask; render_template # type: ignore

app = Flask(__name__)

# --- Données de test (plus tard ce sera une vraie base de données) ---
robots = [
    {
        "id": 1,
        "nom": "Titan MK4",
        "equipe": "Équipe Sigma",
        "annee": 2024,
        "competition": "FRC",
        "classement": 1,
        "description": "Robot polyvalent avec bras articulé et système de vision."
    },
    {
        "id": 2,
        "nom": "Nexus V2",
        "equipe": "Équipe Delta",
        "annee": 2024,
        "competition": "ECAM",
        "classement": 2,
        "description": "Robot rapide spécialisé dans la collecte d'objets."
    },
    {
        "id": 3,
        "nom": "Omega X",
        "equipe": "Équipe Alpha",
        "annee": 2023,
        "competition": "FRC",
        "classement": 3,
        "description": "Robot défensif avec châssis renforcé."
    },
]

# --- Page d'accueil ---
@app.route("/")
def accueil():
    return render_template("accueil.html", robots=robots) # type: ignore

# --- Page détail d'un robot ---
@app.route("/robot/<int:robot_id>")
def detail_robot(robot_id):
    # On cherche le robot avec le bon id
    robot = next((r for r in robots if r["id"] == robot_id), None)
    if robot is None:
        return "Robot introuvable", 404
    return render_template("detail.html", robot=robot) # type: ignore

if __name__ == "__main__":
    app.run(debug=True)
