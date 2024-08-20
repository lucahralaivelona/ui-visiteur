<template>
<main :class="$style.table">
    <section :class="$style.table__header">
        <h1>Gestion de Visiteur</h1>
        <div :class="$style.input-group">
            <input type="search" placeholder="Search Data..." ref="searchInput " />
            <img src="images/search.png" alt="" />
        </div>
        <div style="align-items: center;
    display: flex;">
            <div>
                <!-- <label for="" :class="$style.imgUser"></label> -->
                <button :class="$style.imgUser" @click="
                    showDeleteModal = true;

                  " title="ajouter un visiteur"></button>
                <!-- <img :class="$style.imgUser" src="images/userAdd.png" alt="" @click="showAddModal = true" /> -->

            </div>
            <div :class="$style.export__file">
                <label for="export-file" :class="$style.export__file-btn" title="Export File"></label>
                <input type="checkbox" id="export-file" />
                <div :class="$style.export__file-options">
                    <label>Visualiser le tarif &nbsp; &#10140;</label>
                    <label for="export-file" id="toPDF">Histograme <img src="images/histograme.png" alt="" /></label>
                    <label for="export-file" id="toJSON">Camember <img src="images/pieChart.png" alt="" /></label>
                </div>
            </div>
        </div>

    </section>
    <section :class="$style.table__body">
        <table>
            <thead>
                <tr>
                    <th>Id <span :class="$style.icon-arrow">&UpArrow;</span></th>
                    <th>Nom <span :class="$style.icon-arrow">&UpArrow;</span></th>
                    <th>Nombre de jour<span :class="$style.icon-arrow">&UpArrow;</span></th>
                    <th>Tarif journaliere<span :class="$style.icon-arrow">&UpArrow;</span></th>
                    <th>Tarif <span :class="$style.icon-arrow">&UpArrow;</span></th>
                    <th><span :class="$style.icon-arrow"></span></th>
                    <!-- <th><span :class="$style.icon-arrow"></span></th> -->
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>2</td>
                    <td><img src="images/Jeet Saru.jpg" alt="" /> Jeet Saru</td>
                    <td>Kathmandu</td>
                    <td>27 Aug, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.cancelled]">Cancelled</p>
                    </td>
                    <td><strong>$5350.50</strong></td>
                </tr>
                <tr>
                    <td>3</td>
                    <td><img src="images/Sonal Gharti.jpg" alt="" /> Sonal Gharti</td>
                    <td>Tokyo</td>
                    <td>14 Mar, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.Shipped]">Shipped</p>
                    </td>
                    <td><strong>$210.40</strong></td>
                </tr>
                <tr>
                    <td>4</td>
                    <td><img src="images/Alson GC.jpg" alt="" /> Alson GC</td>
                    <td>New Delhi</td>
                    <td>25 May, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.delivered]">30j</p>
                    </td>
                    <td><strong>$149.70</strong></td>
                </tr>
                <tr>
                    <td>5</td>
                    <td><img src="images/Sarita Limbu.jpg" alt="" /> Sarita Limbu</td>
                    <td>Paris</td>
                    <td>23 Apr, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.pending]">Pending</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>6</td>
                    <td><img src="images/Alex Gonley.jpg" alt="" /> Alex Gonley</td>
                    <td>London</td>
                    <td>23 Apr, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.cancelled]">Cancelled</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>7</td>
                    <td><img src="images/Alson GC.jpg" alt="" /> Jeet Saru</td>
                    <td>New York</td>
                    <td>20 May, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.delivered]">Delivered</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>8</td>
                    <td><img src="images/Sarita Limbu.jpg" alt="" /> Aayat Ali Khan</td>
                    <td>Islamabad</td>
                    <td>30 Feb, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.pending]">Pending</p>
                    </td>
                    <td><strong>$149.70</strong></td>
                </tr>
                <tr>
                    <td>9</td>
                    <td><img src="images/Alex Gonley.jpg" alt="" /> Alson GC</td>
                    <td>Dhaka</td>
                    <td>22 Dec, 2023</td>
                    <td>
                        <p :class="[$style.status, $style.cancelled]">Cancelled</p>
                    </td>
                    <td><strong>$249.99</strong></td>
                </tr>
            </tbody>
        </table>
    </section>
    <section :class="$style.table__footer">
        <div :class="$style.table__footer-content">
            <h4>Tarif total minimal :</h4>
            <p :class="[$style.status, $style.delivered, $style.minMax]">30.000 ar</p>
        </div>

        <div :class="$style.table__footer-content">
            <h4>Tarif total maximal :</h4>
            <p :class="[$style.status, $style.cancelled, $style.minMax]">60.000 ar</p>
        </div>
    </section>
    <div :class="$style.myModal" v-if="showDeleteModal">
        <div :class="$style.modalContainer">
            <div :class="$style.modalHeader">
                <!-- <span :class="$style. soratra">Ajouter un employers</span> -->
                <button :class="[$style.closeBtn, $style.pull-right]" @click="showDeleteModal = false">
                    ×
                </button>
            </div>
            <div :class="$style.modalBody">
                <div :class="$style.container">
                    <div :class="$style.title">Suppresion d'un vol</div>
                    <form action="#">
                        <div :class="$style.user-details">
                            <h4 :class="$style.text-center">
                                Est-tu sur de voiloir supprimer le vol
                            </h4>
                            <div :class="$style.input-box">
                                <h2 :class="$style.text-center">}</h2>
                            </div>
                        </div>

                        <div :class="$style.boutton">
                            <input :class="[$style.btn, $sytle.btn-danger]" value="Supprimer" @click="
                    showDeleteModal = false;

                  " />
                        </div>

                        <div></div>
                    </form>
                </div>
            </div>
        </div>
    </div>

</main>
</template>

<script>
// import "@/assets/css/index.css";
import "@/assets/css/main.css";

export default {
    data() {
        return {
            showDeleteModal: false,

        };
    },

    mounted() {
        this.searchTable();
        this.sortTable();
    },
    methods: {
        searchTable() {
            const search = document.querySelector(".input-group input");
            search.addEventListener("input", this.searchTable);
            const table_rows = document.querySelectorAll("tbody tr");
            table_rows.forEach((row, i) => {
                let table_data = row.textContent.toLowerCase(),
                    search_data = search.value.toLowerCase();

                row.classList.toggle("hide", table_data.indexOf(search_data) < 0);
                row.style.setProperty("--delay", i / 25 + "s");
            });
        },
        sortTable() {
            const table_headings = document.querySelectorAll("thead th");
            const table_rows = document.querySelectorAll("tbody tr");
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
                            .querySelectorAll("td")[column].textContent.toLowerCase(),
                            second_row = b
                            .querySelectorAll("td")[column].textContent.toLowerCase();

                        return sort_asc ?
                            first_row < second_row ?
                            1 :
                            -1 :
                            first_row < second_row ?
                            -1 :
                            1;
                    })
                    .map((sorted_row) =>
                        document.querySelector("tbody").appendChild(sorted_row)
                    );
            }
        },
    },
};
</script>

<style scoped>



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

table {
  width: 100%;
}

td img {
  width: 36px;
  height: 36px;
  margin-right: 0.5rem;
  border-radius: 50%;

  vertical-align: middle;
}

table,
th,
td {
  border-collapse: collapse;
  padding: 1rem;
  text-align: left;
}

thead th {
  position: sticky;
  top: 0;
  left: 0;
  background-color: #d5d1defe;
  cursor: pointer;
  text-transform: capitalize;
}

tbody tr:nth-child(even) {
  background-color: #0000000b;
}

tbody tr {
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
.imgUser:hover{
  background-color: #fff;
  transform: scale(1.15);
  cursor: pointer;
}

.table__footer{
  align-items: center;
  display: flex;
  margin: 20px auto;
  justify-content: space-around;
    


}
.table__footer-content{
  display: flex;
  align-items: center;
  
}

tbody tr.hide {
  opacity: 0;
  transform: translateX(100%);
}

tbody tr:hover {
  background-color: #fff6 !important;
}

tbody tr td,
tbody tr td p,
tbody tr td img {
  transition: 0.2s ease-in-out;
}

tbody tr.hide td,
tbody tr.hide td p {
  padding: 0;
  font: 0 / 0 sans-serif;
  transition: 0.2s ease-in-out 0.5s;
}

tbody tr.hide td img {
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
.status.minMax{
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

thead th span.icon-arrow {
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

thead th:hover span.icon-arrow {
  border: 1.4px solid #6c00bd;
}

thead th:hover {
  color: #6c00bd;
}

thead th.active span.icon-arrow {
  background-color: #6c00bd;
  color: #fff;
}

thead th.asc span.icon-arrow {
  transform: rotate(180deg);
}

thead th.active,
tbody td.active {
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

tbody tr.hidingAfterDelay {
  display: none;
}
tbody tr.hiding {
  opacity: 0 !important;
  transform: translateX(100%) !important;
  /* display: none; */
}

tbody tr.hiding td,
tbody tr.hiding td p {
  padding: 0 !important;
  font: 0 / 0 sans-serif;
  transition: 0.2s ease-in-out 0.5s !important;
}

tbody tr.hiding td img {
  width: 0 !important;
  height: 0 !important;
  transition: 0.2s ease-in-out 0.5s !important;
  /* display: none; */
}


</style>>

