<template>
<main class="table">
    <section class="table__header">
        <h1>Gestion de Visiteur</h1>
        <div class="input-group">
            <input type="search" placeholder="Search Data..." ref="searchInput " />
            <img src="images/search.png" alt="" />
        </div>
        <div style="align-items: center;
    display: flex;">
            <div class="">
                <!-- <label for="" class="imgUser"></label> -->
                <button class="imgUser" @click="
                    showDeleteModal = true;

                  " title="ajouter un visiteur"></button>
                <!-- <img class="imgUser" src="images/userAdd.png" alt="" @click="showAddModal = true" /> -->

            </div>
            <div class="export__file">
                <label for="export-file" class="export__file-btn" title="Export File"></label>
                <input type="checkbox" id="export-file" />
                <div class="export__file-options">
                    <label>Visualiser le tarif &nbsp; &#10140;</label>
                    <label for="export-file" id="toPDF">Histograme <img src="images/histograme.png" alt="" /></label>
                    <label for="export-file" id="toJSON">Camember <img src="images/pieChart.png" alt="" /></label>
                </div>
            </div>
        </div>

    </section>
    <section class="table__body">
        <table>
            <thead>
                <tr>
                    <th>Id <span class="icon-arrow">&UpArrow;</span></th>
                    <th>Nom <span class="icon-arrow">&UpArrow;</span></th>
                    <th>Nombre de jour<span class="icon-arrow">&UpArrow;</span></th>
                    <th>Tarif journaliere<span class="icon-arrow">&UpArrow;</span></th>
                    <th>Tarif <span class="icon-arrow">&UpArrow;</span></th>
                    <th><span class="icon-arrow"></span></th>
                    <!-- <th><span class="icon-arrow"></span></th> -->
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>2</td>
                    <td><img src="images/Jeet Saru.jpg" alt="" /> Jeet Saru</td>
                    <td>Kathmandu</td>
                    <td>27 Aug, 2023</td>
                    <td>
                        <p class="status cancelled">Cancelled</p>
                    </td>
                    <td><strong>$5350.50</strong></td>
                </tr>
                <tr>
                    <td>3</td>
                    <td><img src="images/Sonal Gharti.jpg" alt="" /> Sonal Gharti</td>
                    <td>Tokyo</td>
                    <td>14 Mar, 2023</td>
                    <td>
                        <p class="status shipped">Shipped</p>
                    </td>
                    <td><strong>$210.40</strong></td>
                </tr>
                <tr>
                    <td>4</td>
                    <td><img src="images/Alson GC.jpg" alt="" /> Alson GC</td>
                    <td>New Delhi</td>
                    <td>25 May, 2023</td>
                    <td>
                        <p class="status delivered">30j</p>
                    </td>
                    <td><strong>$149.70</strong></td>
                </tr>
                <tr>
                    <td>5</td>
                    <td><img src="images/Sarita Limbu.jpg" alt="" /> Sarita Limbu</td>
                    <td>Paris</td>
                    <td>23 Apr, 2023</td>
                    <td>
                        <p class="status pending">Pending</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>6</td>
                    <td><img src="images/Alex Gonley.jpg" alt="" /> Alex Gonley</td>
                    <td>London</td>
                    <td>23 Apr, 2023</td>
                    <td>
                        <p class="status cancelled">Cancelled</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>7</td>
                    <td><img src="images/Alson GC.jpg" alt="" /> Jeet Saru</td>
                    <td>New York</td>
                    <td>20 May, 2023</td>
                    <td>
                        <p class="status delivered">Delivered</p>
                    </td>
                    <td><strong>$399.99</strong></td>
                </tr>
                <tr>
                    <td>8</td>
                    <td><img src="images/Sarita Limbu.jpg" alt="" /> Aayat Ali Khan</td>
                    <td>Islamabad</td>
                    <td>30 Feb, 2023</td>
                    <td>
                        <p class="status pending">Pending</p>
                    </td>
                    <td><strong>$149.70</strong></td>
                </tr>
                <tr>
                    <td>9</td>
                    <td><img src="images/Alex Gonley.jpg" alt="" /> Alson GC</td>
                    <td>Dhaka</td>
                    <td>22 Dec, 2023</td>
                    <td>
                        <p class="status cancelled">Cancelled</p>
                    </td>
                    <td><strong>$249.99</strong></td>
                </tr>
            </tbody>
        </table>
    </section>
    <section class="table__footer">
        <div class="table__footer-content">
            <h4>Tarif total minimal :</h4>
            <p class="status delivered minMax">30.000 ar</p>
        </div>

        <div class="table__footer-content">
            <h4>Tarif total maximal :</h4>
            <p class="status cancelled minMax">60.000 ar</p>
        </div>
    </section>
    <div class="myModal" v-if="showDeleteModal">
        <div class="modalContainer">
            <div class="modalHeader">
                <!-- <span class=" soratra">Ajouter un employers</span> -->
                <button class="closeBtn pull-right" @click="showDeleteModal = false">
                    ×
                </button>
            </div>
            <div class="modalBody">
                <div class="container">
                    <div class="title">Suppresion d'un vol</div>
                    <form action="#">
                        <div class="user-details">
                            <h4 class="text-center">
                                Est-tu sur de voiloir supprimer le vol
                            </h4>
                            <div class="input-box">
                                <h2 class="text-center"></h2>
                            </div>
                        </div>

                        <div class="boutton">
                            <input class="btn btn-danger" value="Supprimer" @click="
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
import "@/assets/css/index.css";

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

<style module>
</style>
