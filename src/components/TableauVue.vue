<template>
  <main :class="$style.table">
    <section :class="$style.table__header">
      <h1 style="">Gestion de Visiteur</h1>
      <div :class="$style['input-group']">
        <input
          style=""
          type="search"
          placeholder="Recherche optimisé..."
          ref="searchInput "
          data-role="search-input"
        />
        <img src="images/search.png" alt="" />
      </div>
      <div style="align-items: center; display: flex">
        <div style="">
          <button
            @click="showModal"
            :class="$style.imgUser"
            title="ajouter un visiteur"
          ></button>
        </div>
        <div :class="$style.export__file">
          <label
            for="export-file"
            :class="$style['export__file-btn']"
            title="Export File"
          ></label>
          <input style="" type="checkbox" id="export-file" />
          <div :class="$style['export__file-options']">
            <label style="">Visualiser le tarif &nbsp; &#10140;</label>
            <label
              style=""
              @click="showHistogramme(), chartHistogramme()"
              for="export-file"
              id="toPDF"
              >Histograme
              <img
                src="images/histograme.png"
                @click="showHistogramme(), chartHistogramme()"
                alt=""
            /></label>
            <label
              style=""
              @click="showPie(), chartPie()"
              for="export-file"
              id="toJSON"
              >Camember
              <img
                @click="showPie(), chartPie()"
                src="images/pieChart.png"
                alt=""
            /></label>
          </div>
        </div>
      </div>
    </section>
    <section :class="$style.table__body">
      <table :class="$style['mainTable']">
        <thead :class="$style['tableauThead']">
          <tr :class="$style['tableauTrHeader']">
            
            <th></th>
            <th data-role="sort-header">
              Nom <span :class="$style['icon-arrow']">&UpArrow;</span>
            </th>

            <th data-role="sort-header">
              Nombre de jour<span :class="$style['icon-arrow']">&UpArrow;</span>
            </th>
            <th data-role="sort-header">
              Tarif journaliere<span :class="$style['icon-arrow']"
                >&UpArrow;</span
              >
            </th>
            <th data-role="sort-header">
              Tarif <span :class="$style['icon-arrow']">&UpArrow;</span>
            </th>
            <th data-role="sort-header">
              <span :class="$style['icon-arrow']"></span>
            </th>
            <th data-role="sort-header">
              <span :class="$style['icon-arrow']"></span>
            </th>
            <!-- <th><span :class="$style.icon-arrow"></span></th> -->
          </tr>
        </thead>
        <tbody :class="$style['tableauTbody']">
          <tr v-for="member in members" :key="member._id" data-role="table-row">
          
            <td>
              <img :class="$style['tdImg']" src="images/Jeet Saru.jpg" alt="" />
            </td>
            <td>{{ member.nom }}</td>
            <td>{{ member.nombreDeJour }}</td>
            <td>{{ member.tarifJournalier }}</td>
            <td>{{ member.tarifJournalier * member.nombreDeJour }}</td>

            <td>
              <img
                class="imgGar"
                @click="
                  showEditModal();
                  selectMember(member);
                "
                src="images/document.png"
                alt=""
              />
            </td>
            <td>
              <img
                class="imgGar"
                @click="
                  showDeletModal();
                  selectMember(member);
                "
                src="images/supprimer.png"
                alt=""
              />
            </td>
          </tr>
        </tbody>
      </table>
    </section>
    <section :class="$style.table__footer">
      <div :class="$style['table__footer-content']">
        <h4>Tarif maximal :</h4>
        <p :class="[$style.status, $style.delivered, $style.minMax]">
          {{ maximum }}ar
        </p>
      </div>

      <div :class="$style['table__footer-content']">
        <h4>Tarif minimal :</h4>
        <p :class="[$style.status, $style.cancelled, $style.minMax]">
          {{ minimum }} ar
        </p>
      </div>
      <div :class="$style['table__footer-content']">
        <h4>Tarif Total:</h4>
        <p :class="[$style.status, $style.pending, $style.minMax]">
          {{ total }} ar
        </p>
      </div>
    </section>
    <section>
      <modal
        name="ajouterUtilisateur"
        height="auto"
        :scrollable="true"
        :shiftX="0.4"
        :shiftY="0.5"
      >
        <div class="container">
          <div class="title">Ajout d'utilisateur</div>
          <form action="#">
            <div class="user-details">
              <div class="input-box">
                <span class="details">Nom</span>
                <input
                  type="text"
                  placeholder="Entrer le nom du visiteur"
                  required
                  v-model="newMember.nom"
                />
              </div>

              <div class="input-box">
                <span class="details">Nombre de jour de son sejour</span>
                <input
                  type="number"
                  placeholder="Entrer le nombre de jour de son sejour "
                  required
                  v-model="newMember.nombreDeJour"
                />
              </div>

              <div class="input-box">
                <span class="details">Tarif journalier</span>
                <input
                  type="number"
                  placeholder="Entrer le tarif Journalier"
                  required
                  v-model="newMember.tarifJournalier"
                />
              </div>
            </div>

            <div class="boutton">
              <input
                type="submit"
                value="enregistrer"
                @click="
                  hideModal();
                  saveMember();
                "
              />
            </div>

            <div></div>
          </form>
        </div>
      </modal>
      <modal
        name="modifierUtilisateur"
        height="auto"
        :scrollable="true"
        :shiftX="0.4"
        :shiftY="0.5"
      >
        <div class="container">
          <div class="title">Modifier utilisateur</div>
          <form action="#">
            <div class="user-details">
              <div class="input-box">
                <span class="details">Nom</span>
                <input
                  type="text"
                  placeholder="Entrer le nom du visiteur"
                  required
                  v-model="clickMember.nom"
                />
              </div>

              <div class="input-box">
                <span class="details">Nombre de jour de son sejour</span>
                <input
                  type="number"
                  placeholder="Entrer le nombre de jour de son sejour "
                  required
                  v-model="clickMember.nombreDeJour"
                />
              </div>

              <div class="input-box">
                <span class="details">Tarif journalier</span>
                <input
                  type="number"
                  placeholder="Entrer le tarif Journalier"
                  required
                  v-model="clickMember.tarifJournalier"
                />
              </div>
            </div>

            <div class="boutton">
              <input
                type="submit"
                value="Modifier"
                @click="
                  hideUpdateModal();
                  EditMember();
                "
              />
            </div>

            <div></div>
          </form>
        </div>
      </modal>
      <modal
        name="histogramme"
        height="auto"
        :scrollable="true"
        :shiftX="0.4"
        :shiftY="0.5"
      >
        <h3>Histograme</h3>
        <div class="container">
          <canvas ref="chartCanvas"></canvas>
        </div>
      </modal>
      <modal
        name="pie"
        height="auto"
        :scrollable="true"
        :shiftX="0.4"
        :shiftY="0.5"
      >
        <h3>Camembert</h3>

        <div class="container">
          <canvas ref="chartCanvasPie"></canvas>
        </div>
      </modal>

      <modal
        name="supprimerUtilisateur"
        height="auto"
        :scrollable="true"
        :shiftX="0.4"
        :shiftY="0.5"
      >
        <div class="container">
          <div class="title">Suprresion d'utilisateur</div>
          <form action="#">
            <div class="user-details">
              <div class="input-box">
                <h4>Veux tu supprimer {{ clickMember.nom }}?</h4>
              </div>
            </div>

            <div class="boutton">
              <input
                type="submit"
                value="Supprimer"
                @click="
                  hideDeletModal();
                  deleteMember();
                  getAllMembers();
                "
              />
            </div>

            <div></div>
          </form>
        </div>
      </modal>
    </section>
  </main>
</template>

<script>
// import "@/assets/css/index.css";
import "@/assets/css/main.css";
import axios from "axios";
// import Swal from "sweetalert";
import Swal from "sweetalert2";
import Chart from "chart.js/auto";

export default {
  components: {
    // Modal
  },
  data() {
    return {
      chart: null,
      chartData: null,
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
      },

      errorMessage: "",
      successMessage: "",
      members: [],
      totalValueData: [],
      newMember: {
        // numVisiteur: "",
        nom: "",
        nombreDeJour: "",
        tarifJournalier: "",
      },
      clickMember: {},
    };
  },

  mounted() {
    this.searchTable();
    this.sortTable();
    this.getAllMembers();
  },
  methods: {
    showHistogramme() {
      this.$modal.show("histogramme");
      this.chartHistogramme();
    },
    showPie() {
      this.$modal.show("pie");
      this.chartPie();
    },

    showModal() {
      this.$modal.show("ajouterUtilisateur");
    },
    hideModal() {
      this.$modal.hide("ajouterUtilisateur");
    },
    showEditModal() {
      this.$modal.show("modifierUtilisateur");
    },
    hideUpdateModal() {
      this.$modal.hide("modifierUtilisateur");
    },
    showDeletModal() {
      this.$modal.show("supprimerUtilisateur");
    },
    hideDeletModal() {
      this.$modal.hide("supprimerUtilisateur");
    },

    showSuccessAlert() {
      Swal.fire({
        icon: "success",
        title: "Visiteur repertorier dans la base",
        // text: "Vol ajouté à la base",  // Cela n'est pas nécessaire car vous avez déjà un titre
        toast: true,
        position: "top-end",
        showConfirmButton: false,
        timer: 4000,
      });
    },

    showEditAlert() {
      Swal.fire({
        icon: "success",
        title: "Modification d'information du visiteur avec succès !",
        // text: "Vol ajouté à la base",  // Cela n'est pas nécessaire car vous avez déjà un titre
        toast: true,
        position: "top-end",
        showConfirmButton: false,
        timer: 4000,
      });
    },

    showDeleteAlert() {
      Swal.fire({
        icon: "success",
        title: "Visiteur supprimer avec succès !",
        // text: "Vol ajouté à la base",  // Cela n'est pas nécessaire car vous avez déjà un titre
        toast: true,
        position: "top-end",
        showConfirmButton: false,
        timer: 4000,
      });
    },
    getAllMembers() {
      axios
        .get("https://visiteur.onrender.com/api/v1/visiteurs")
        .then((response) => {
          if (response.data.error) {
            this.errorMessage = response.data.message;
          } else {
            this.members = response.data;
            console.log(response.data);
            this.getMinMax();
          }
        });
    },
    getMinMax() {
      var members = this.members;

      const totalValueData = members.map(
        (obj) => obj.tarifJournalier * obj.nombreDeJour
      ); // Calculer le minimum, le total et le maximum des données
      const minimum = Math.min(...totalValueData);
      const maximum = Math.max(...totalValueData);
      const total = totalValueData.reduce((acc, cur) => acc + cur, 0);
      this.minimum = minimum;
      this.maximum = maximum;
      this.total = total;
      console.log(this.minimum, this.maximum);
    },

    chartHistogramme() {
      var members = this.members;

      const totalValueData = members.map(
        (obj) => obj.tarifJournalier * obj.nombreDeJour
      ); // Calculer le minimum, le total et le maximum des données
      const minimum = Math.min(...totalValueData);
      const total = totalValueData.reduce((acc, cur) => acc + cur, 0);
      const maximum = Math.max(...totalValueData);

      const ctx = this.$refs.chartCanvas.getContext("2d");
      this.chart = new Chart(ctx, {
        type: "bar",
        data: {
          labels: ["valeur minimum", "valeur maximum", "valeur total"],
          datasets: [
            {
              label: "",
              backgroundColor: ["crimson", "lightblue", "lightgreen"],
              borderColor: "rgba(75, 192, 192, 1)",
              borderWidth: 1,
              data: [minimum, maximum, total],
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          legend: {
            display: true,
            position: "top",
            labels: {
              fontColor: "#333",
              fontSize: 14,
              boxWidth: 20,
              usePointStyle: true,
            },
            fullWidth: true,
          },
          title: {
            display: true,
            text: `Statistics: Min = ${minimum}, Total = ${total}, Max = ${maximum}`,
            fontSize: 18,
            fontColor: "#333",
            fontStyle: "normal",
          },
        },
      });
    },
    chartPie() {
      var members = this.members;

      const totalValueData = members.map(
        (obj) => obj.tarifJournalier * obj.nombreDeJour
      ); // Calculer le minimum, le total et le maximum des données
      const minimum = Math.min(...totalValueData);
      const total = totalValueData.reduce((acc, cur) => acc + cur, 0);
      const maximum = Math.max(...totalValueData);

      const ctx = this.$refs.chartCanvasPie.getContext("2d");
      this.chart = new Chart(ctx, {
        type: "pie",
        data: {
          labels: ["valeur minimum", "valeur maximum", "valeur total"],
          datasets: [
            {
              label: "Valeur en ariary",
              backgroundColor: ["crimson", "lightblue", "lightgreen"],
              borderColor: "rgba(75, 192, 192, 1)",
              borderWidth: 1,
              data: [minimum, maximum, total],
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          legend: {
            display: true,
            position: "top",
            labels: {
              fontColor: "#333",
              fontSize: 14,
              boxWidth: 20,
              usePointStyle: true,
            },
            fullWidth: true,
          },
          title: {
            display: true,
            text: `Statistics: Min = ${minimum}, Total = ${total}, Max = ${maximum}`,
            fontSize: 18,
            fontColor: "#333",
            fontStyle: "normal",
          },
        },
      });
    },
    saveMember() {
      axios
        .post(
          "https://visiteur.onrender.com/api/v1/visiteurs",
          {
            // numVisiteur: this.newMember.numVisiteur,
            nom: this.newMember.nom,
            nombreDeJour: this.newMember.nombreDeJour,
            tarifJournalier: this.newMember.tarifJournalier,
          },
          {
            headers: {
              "Content-Type": "application/json",
            },
          }
        )
        .then((response) => {
          this.newMember = {
            nom: "",
            nombreDeJour: "",
            tarifJournaliers: "",
          };
          if (response.data.error) {
            this.errorMessage = response.data.message;
          } else {
            this.successMessage = response.data.message;
            this.getAllMembers();
            this.showSuccessAlert(response.data.message);
          }
        })
        .catch((error) => {
          this.errorMessage = "Une erreur s'est produite lors de l'ajout.";
          console.error(error);
        });
    },

    EditMember() {
      axios
        .put(
          `https://visiteur.onrender.com/api/v1/visiteurs/${this.clickMember._id}`,
          {
            // numVisiteur: this.clickMember.numVisiteur,
            nom: this.clickMember.nom,
            nombreDeJour: this.clickMember.nombreDeJour,
            tarifJournalier: this.clickMember.tarifJournalier,
          },
          {
            headers: {
              "Content-Type": "application/json",
            },
          }
        )
        .then((response) => {
          this.clickMember = {};
          if (response.data.error) {
            this.errorMessage = response.data.message;
          } else {
            this.successMessage = response.data.message;
            this.getAllMembers();
            this.showEditAlert(response.data.message);
          }
        })
        .catch((error) => {
          this.errorMessage =
            "Une erreur s'est produite lors de la mise à jour.";
          console.error(error);
        });
    },
    deleteMember() {
      axios
        .delete(
          `https://visiteur.onrender.com/api/v1/visiteurs/${this.clickMember._id}`
        )
        .then((response) => {
          this.clickMember = {};
          if (response.data.error) {
            this.errorMessage = response.data.message;
          } else {
            this.successMessage = response.data.message;
            this.getAllMembers();
            this.showDeleteAlert(response.data.message);
          }
        })
        .catch((error) => {
          this.errorMessage =
            "Une erreur s'est produite lors de la suppression.";
          console.error(error);
        });
    },
    selectMember(member) {
      this.clickMember = member;
    },

    searchTable() {
      const search = document.querySelector('[data-role="search-input"]');
      search.addEventListener("input", this.searchTable);
      const table_rows = document.querySelectorAll('[data-role="table-row"]');
      table_rows.forEach((row, i) => {
        let table_data = row.textContent.toLowerCase(),
          search_data = search.value.toLowerCase();

        row.classList.toggle(
          "TableauVue_hide_BOrSV",
          table_data.indexOf(search_data) < 0
        );
        row.style.setProperty("--delay", i / 25 + "s");
      });
    },
    sortTable() {
      const table_headings = document.querySelectorAll(".tableauTrHeader th");
      const table_rows = document.querySelectorAll(".tableauTbody tr");
      // const table_headings = document.querySelectorAll("thead th");
      // const table_rows = document.querySelectorAll("tbody tr");
      table_headings.forEach((head, i) => {
        let sort_asc = true;
        head.onclick = () => {
          table_headings.forEach((head) => head.classList.remove("active"));
          head.classList.add("active");

          document
            .querySelectorAll("td")
            .forEach((td) => td.classList.remove("active"));
          table_rows.forEach((row) => {
            row.querySelectorAll("td")[i].classList.add("active");
          });

          head.classList.toggle("asc", sort_asc);
          sort_asc = head.classList.contains("asc") ? false : true;

          sortTable(i, sort_asc);
        };
      });

      function sortTable(column, sort_asc) {
        [...table_rows]
          .sort((a, b) => {
            let first_row = a
                .querySelectorAll(".tableauTbody td")[column].textContent.toLowerCase(),
              second_row = b
                .querySelectorAll(".tableauTbody td")[column].textContent.toLowerCase();

            return sort_asc
              ? first_row < second_row
                ? 1
                : -1
              : first_row < second_row
              ? -1
              : 1;
          })
          .map((sorted_row) =>
            document.querySelector(".tableauTbody").appendChild(sorted_row)
          );
      }
    },
  },
};
</script>

<style>
.imgButtonBordure {
  border: none;
  border-radius: 50%;
}

.imgGar {
  width: 36px;
  height: 36px;

  vertical-align: middle;
}

.container {
  max-width: 700px;
  width: 100%;
  background: #fff;
  padding: 25px 30px;
  border-radius: 5px;
}

.container .title {
  font-size: 25px;
  font-weight: 500;
  position: relative;
}

.container .title::before {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  height: 3px;
  width: 30px;
  background: linear-gradient(135deg, #71b7e6, #9b59b6);
}

.container form .user-details {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 20px 0 12px 0;
  max-height: 300px;
  /* La hauteur maximale avant que la barre de défilement ne soit activée */
  overflow-y: auto;
}

form .user-details .input-box {
  margin-bottom: 15px;
  width: calc(100% / 2 - 20px);
}

.user-details .input-box .details {
  display: block;
  font-weight: 500;
  margin-bottom: 5px;
}

.user-details .input-box select {
  height: 45px;
  width: 100%;
  outline: none;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding-left: 15px;
  font-size: 16px;
  border-bottom-width: 2px;
  -webkit-transition: all 0.3s ease;
  transition: all 0.3s ease;
}

.user-details .input-box input {
  height: 45px;
  width: 100%;
  outline: none;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding-left: 15px;
  font-size: 16px;
  border-bottom-width: 2px;
  transition: all 0.3s ease;
}

.user-details .input-box input:focus,
.user-details .input-box input:valid {
  border-color: #9b59b6;
}

form .gender-details .gender-title {
  font-size: 20px;
  font-weight: 500;
}

form .gender-details .category {
  display: flex;
  width: 80%;
  margin: 14px 0;
  justify-content: space-between;
}

.gender-details .category label {
  display: flex;
  align-items: center;
}

.gender-details .category .dot {
  height: 18px;
  width: 18px;
  background: #d9d9d9;
  border-radius: 50%;
  margin-right: 10px;
  border: 5px solid transparent;
  transition: all 0.3s ease;
}

#dot-1:checked ~ .category label .one,
#dot-2:checked ~ .category label .two {
  border-color: #d9d9d9d9;
  background: #9b59b6;
}

form input[type="radio"] {
  display: none;
}

form .boutton {
  height: 45px;
  margin: 45px 0;
}

form .boutton input {
  height: 100%;
  width: 100%;
  outline: none;
  color: #fff;
  border: none;
  font-size: 18px;
  font-weight: 5px;
  border-radius: 5px;
  letter-spacing: 1px;
  background: linear-gradient(135deg, #71b7e6, #9b59b6);
}

form .boutton input:hover {
  background: linear-gradient(135deg, #71b7e6, #9b59b6);
}

@media (max-width: 584px) {
  .container {
    max-width: 100%;
  }

  form .user-details .input-box {
    margin-bottom: 15px;
    width: 100%;
  }

  form .gender-details .category {
    width: 100%;
  }

  .container form .user-details {
    max-height: 300px;
    overflow-y: scroll;
  }

  /* .user-details::-webkit-scrollbar{
    width: 0;   
 }  */
}
</style>
<style module>
.custom-modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
}

main.table {
  width: 82vw;
  height: 90vh;
  background-color: #fff5;

  backdrop-filter: blur(7px);
  box-shadow: 0 0.4rem 0.8rem #0005;
  border-radius: 0.8rem;

  overflow: hidden;
}

.table__header {
  width: 100%;
  height: 10%;
  background-color: #fff4;
  padding: 0.8rem 1rem;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.table__header .input-group {
  width: 35%;
  height: 100%;
  background-color: #fff5;
  padding: 0 0.8rem;
  border-radius: 2rem;

  display: flex;
  justify-content: center;
  align-items: center;

  transition: 0.2s;
}

.table__header .input-group:hover {
  width: 45%;
  background-color: #fff8;
  box-shadow: 0 0.1rem 0.4rem #0002;
}

.table__header .input-group img {
  width: 1.2rem;
  height: 1.2rem;
}

.table__header .input-group input {
  width: 100%;
  padding: 0 0.5rem 0 0.3rem;
  background-color: transparent;
  border: none;
  outline: none;
}

.table__body {
  width: 95%;
  max-height: calc(89% - 5rem);
  background-color: #fffb;

  margin: 0.8rem auto;
  border-radius: 0.6rem;

  overflow: auto;
  overflow: overlay;
  /*  esorina rehefa ampiasaina */
  min-height: 483.351px;
}

.table__body::-webkit-scrollbar {
  width: 0.5rem;
  height: 0.5rem;
}

.table__body::-webkit-scrollbar-thumb {
  border-radius: 0.5rem;
  background-color: #0004;
  visibility: hidden;
}

.table__body:hover::-webkit-scrollbar-thumb {
  visibility: visible;
}

.mainTable {
  width: 100%;
}

.tdImg {
  width: 36px;
  height: 36px;
  margin-right: 0.5rem;
  border-radius: 50%;

  vertical-align: middle;
}

.mainTable,
.tableauThead th,
.table__body td {
  border-collapse: collapse;
  padding: 1rem;
  text-align: left;
}

.tableauThead th {
  position: sticky;
  top: 0;
  left: 0;
  background-color: #d5d1defe;
  cursor: pointer;
  text-transform: capitalize;
}

.tableauTbody tr:nth-child(even) {
  background-color: #0000000b;
}

.tableauTbody tr {
  --delay: 0.1s;
  transition: 0.5s ease-in-out var(--delay), background-color 0s;
}

.imgUser {
  /* width: 45px;
  height: 45px; */
  display: inline-block;
  width: 2rem;
  height: 2rem;
  background: #fff6 url(images/userAdd.png) center / 80% no-repeat;
  border-radius: 50%;
  transition: 0.2s ease-in-out;
  vertical-align: middle;
  border: none;
  margin-right: 20px;
}

.imgUser:hover {
  background-color: #fff;
  transform: scale(1.15);
  cursor: pointer;
}

.table__footer {
  align-items: center;
  display: flex;
  margin: 20px auto;
  justify-content: space-around;
}

.table__footer-content {
  display: flex;
  align-items: center;
}

.tableauTbody tr.hide {
  opacity: 0;
  transform: translateX(100%);
}

.tableauTbody tr:hover {
  background-color: #fff6 !important;
}

.tableauTbody tr td,
.tableauTbody tr td p,
.tableauTbody tr td img {
  transition: 0.2s ease-in-out;
}

.tableauTbody tr.hide td,
.tableauTbody tr.hide td p {
  padding: 0;
  font: 0 / 0 sans-serif;
  transition: 0.2s ease-in-out 0.5s;
}

.tableauTbody tr.hide td img {
  width: 0;
  height: 0;
  transition: 0.2s ease-in-out 0.5s;
}

.status {
  padding: 0.4rem 0;
  border-radius: 2rem;
  text-align: center;
}

.status.delivered {
  background-color: #86e49d;
  color: #006b21;
}

.status.cancelled {
  background-color: #d893a3;
  color: #b30021;
}

.status.minMax {
  padding-left: 10px;
  padding-right: 10px;
  margin-left: 10px;
}

/* .status.delivered.min{
  padding-left: 10px;
  padding-right: 10px;
} */

.status.pending {
  background-color: #ebc474;
}

.status.shipped {
  background-color: #6fcaea;
}

@media (max-width: 1000px) {
  td:not(:first-of-type) {
    min-width: 12.1rem;
  }
}

.tableauThead th span.icon-arrow {
  display: inline-block;
  width: 1.3rem;
  height: 1.3rem;
  border-radius: 50%;
  border: 1.4px solid transparent;

  text-align: center;
  font-size: 1rem;

  margin-left: 0.5rem;
  transition: 0.2s ease-in-out;
}

.tableauThead th:hover span.icon-arrow {
  border: 1.4px solid #6c00bd;
}

.tableauThead th:hover {
  color: #6c00bd;
}

.tableauThead th.active span.icon-arrow {
  background-color: #6c00bd;
  color: #fff;
}

.tableauThead th.asc span.icon-arrow {
  transform: rotate(180deg);
}

.tableauThead th.active,
.tableauTbody td.active {
  color: #6c00bd;
}

.export__file {
  position: relative;
}

.export__file .export__file-btn {
  display: inline-block;
  width: 2rem;
  height: 2rem;
  background: #fff6 url(images/export.png) center / 80% no-repeat;
  border-radius: 50%;
  transition: 0.2s ease-in-out;
}

.export__file .export__file-btn:hover {
  background-color: #fff;
  transform: scale(1.15);
  cursor: pointer;
}

.export__file input {
  display: none;
}

.export__file .export__file-options {
  position: absolute;
  right: 0;

  width: 12rem;
  border-radius: 0.5rem;
  overflow: hidden;
  text-align: center;

  opacity: 0;
  transform: scale(0.8);
  transform-origin: top right;

  box-shadow: 0 0.2rem 0.5rem #0004;

  transition: 0.2s;
}

.export__file input:checked + .export__file-options {
  opacity: 1;
  transform: scale(1);
  z-index: 100;
}

.export__file .export__file-options label {
  display: block;
  width: 100%;
  padding: 0.6rem 0;
  background-color: #f2f2f2;

  display: flex;
  justify-content: space-around;
  align-items: center;

  transition: 0.2s ease-in-out;
}

.export__file .export__file-options label:first-of-type {
  padding: 1rem 0;
  background-color: #86e49d !important;
}

.export__file .export__file-options label:hover {
  transform: scale(1.05);
  background-color: #fff;
  cursor: pointer;
}

.export__file .export__file-options img {
  width: 2rem;
  height: auto;
}

.tableauTbody tr.hidingAfterDelay {
  display: none;
}

.tableauTbody tr.hiding {
  opacity: 0 !important;
  transform: translateX(100%) !important;
  /* display: none; */
}

.tableauTbody tr.hiding td,
.tableauTbody tr.hiding td p {
  padding: 0 !important;
  font: 0 / 0 sans-serif;
  transition: 0.2s ease-in-out 0.5s !important;
}

.tableauTbody tr.hiding td img {
  width: 0 !important;
  height: 0 !important;
  transition: 0.2s ease-in-out 0.5s !important;
  /* display: none; */
}
</style>
