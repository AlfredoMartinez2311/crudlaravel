<template>
    <div id="appAlumno">
        <div class="row">
            <div class="col-12 col-md-6">
                <div class="card">
                    <div class="card-header">REGISTRO DE ALUMNO</div>
                    <div class="card-body">
                        <form id="frmAlumno" @reset.prevent="nuevoAlumno" v-on:submit.prevent="guardarAlumno">
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtCodigoAlumno">CODIGO:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[US|SM]{2}[IS|LI]{2}[0-9]{6}"
                                        title="Ingrese un codigo de alumno de 3 digitos" v-model="alumno.codigo" type="text"
                                        class="form-control" name="txtCodigoAlumno" id="txtCodigoAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtNombreAlumno">NOMBRE:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[A-Za-zÑñáéíóú ]{3,75}" v-model="alumno.nombre" type="text"
                                        class="form-control" name="txtNombreAlumno" id="txtNombreAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtFechaAlumno">Fecha de Nacimiento:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required v-model="alumno.fecha" type="date" class="form-control"
                                        name="txtFechaAlumno" id="txtFechaAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtDireccionAlumno">DIRECCION:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[A-Za-zÑñáéíóú ]{3,75}" v-model="alumno.direccion" type="text"
                                        class="form-control" name="txtDireccionAlumno" id="txtDireccionAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtMunicipioAlumno">Municipio:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[A-Za-zÑñáéíóú ]{3,75}" v-model="alumno.municipio" type="text"
                                        class="form-control" name="txtMunicipioAlumno" id="txtMunicipioAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtNDepartamentoAlumno">Departamento:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[A-Za-zÑñáéíóú ]{3,75}" v-model="alumno.departamento"
                                        type="text" class="form-control" name="txtNDepartamentoAlumno"
                                        id="txtNDepartamentoAlumno">
                                </div>
                            </div>

                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtTelefonoAlumno">TELEFONO:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[0-9]{4}-[0-9]{4}" v-model="alumno.telefono" type="text"
                                        class="form-control" name="txtTelefonoAlumno" id="txtTelefonoAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtDuiAlumno">DUI:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <input required pattern="[0-9]{8}-[0-9]{1}" v-model="alumno.dui" type="text"
                                        class="form-control" name="txtDuiAlumno" id="txtDuiAlumno">
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-4 col-md-4">
                                    <label for="txtSexoAlumno">Sexo:</label>
                                </div>
                                <div class="col-6 col-md-6">
                                    <select required v-model="alumno.sexo" class="form-control" name="txtSexoAlumno"
                                        id="txtSexoAlumno">
                                        <option value="Masculino">Hombre</option>
                                        <option value="Femenino">Mujer</option>
                                    </select>
                                </div>
                            </div>
                            <div class="row p-1">
                                <div class="col-3 col-md-3">
                                    <input class="btn btn-primary" type="submit" value="Guardar">
                                </div>
                                <div class="col-3 col-md-3">
                                    <input class="btn btn-warning" type="reset" value="Nuevo">
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
            <div class="col-12 col-md-6">
                <div class="card">
                    <div class="card-header">LISTADO DE ALUMNOS</div>
                    <div class="card-body">
                        <table class="table table-bordered table-hover">
                            <thead>
                                <tr>
                                    <th>BUSCAR:</th>
                                    <th colspan="2"><input type="text" class="form-control" v-model="buscar"
                                            @keyup="listar()" placeholder="Buscar "></th>
                                </tr>
                                <tr>
                                    <th>CODIGO</th>
                                    <th>NOMBRE</th>
                                    <th>FECHA DE NACIMIENTO</th>
                                    <th>DIRECCION</th>
                                    <th>MUNICIPIO</th>
                                    <th>DEPARTAMENTO</th>
                                    <th>TELEFONO</th>
                                    <th>DUI</th>
                                    <th>SEXO</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="alumno in alumnos" :key="alumno.idAlumno" @click="modificarAlumno(alumno)">
                                    <td>{{ alumno.codigo }}</td>
                                    <td>{{ alumno.nombre }}</td>
                                    <td>{{ alumno.fecha }}</td>
                                    <td>{{ alumno.direccion }}</td>
                                    <td>{{ alumno.municipio }}</td>
                                    <td>{{ alumno.departamento }}</td>
                                    <td>{{ alumno.telefono }}</td>
                                    <td>{{ alumno.dui }}</td>
                                    <td>{{ alumno.sexo }}</td>
                                    <td><button class="btn btn-danger" @click="eliminarAlumno(alumno)">ELIMINAR</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    props: ['form'],
    data() {
        return {
            accion: 'nuevo',
            buscar: '',
            alumnos: [],
            alumno: {
                idAlumno: '',
                codigo: '',
                nombre: '',
                fecha: '',
                direccion: '',
                municipio: '',
                departamento: '',
                telefono: '',
                dui: '',
                sexo: '',
            }
        }
    },
    methods: {
        async guardarAlumno() {
            this.listar();
            let method = 'POST';
            if (this.accion === 'nuevo') {
                this.alumno.idAlumno = new Date().getTime().toString(16);
                this.alumnos.push(JSON.parse(JSON.stringify(this.alumno)));
                method = 'POST';
            } else if (this.accion === 'modificar') {
                let index = this.alumnos.findIndex(alumno => alumno.idAlumno == this.alumno.idAlumno);
                this.alumnos[index] = JSON.parse(JSON.stringify(this.alumno));
                method = 'PUT';
            } else if (this.accion === 'eliminar') {
                let index = this.alumnos.findIndex(alumno => alumno.idAlumno == this.alumno.idAlumno);
                this.alumnos.splice(index, 1);
                method = 'DELETE';
            }
            localStorage.setItem("alumnos", JSON.stringify(this.alumnos));
            await axios({
                url: '/alumnos',
                method,
                data: this.alumno
            }).then(resp => {
                console.log('exito', resp);
            }).catch(err => {
                console.log('error', err);
            });
            this.nuevoAlumno();
        },
        eliminarAlumno(alumno) {
            if (confirm(`Esta seguro de eliminar a ${alumno.nombre}?`)) {
                this.accion = 'eliminar';
                this.alumno = alumno;
                this.guardarAlumno();
            }
        },
        nuevoAlumno() {
            this.accion = 'nuevo';
            this.alumno.idAlumno = '';
            this.alumno.codigo = '';
            this.alumno.nombre = '';
            this.alumno.fecha = '';
            this.alumno.direccion = '';
            this.alumno.municipio = '';
            this.alumno.departamento = '';
            this.alumno.telefono = '';
            this.alumno.dui = '';
            this.alumno.sexo = '';
        },
        modificarAlumno(alumno) {
            this.accion = 'modificar';
            this.alumno = alumno;
        },
        listar() {

            this.alumnos = JSON.parse(localStorage.getItem('alumnos') || "[]")
                .filter(alumno => alumno.nombre.toLowerCase().indexOf(this.buscar.toLowerCase()) > -1 ||
                    alumno.codigo.indexOf(this.buscar) > -1 ||
                    alumno.fecha.indexOf(this.buscar) > -1 ||
                    alumno.direccion.indexOf(this.buscar) > -1 ||
                    alumno.departamento.indexOf(this.buscar) > -1 ||
                    alumno.telefono.indexOf(this.buscar) > -1 ||
                    alumno.dui.indexOf(this.buscar) > -1 ||
                    alumno.sexo.indexOf(this.buscar) > -1 ||
                    alumno.municipio.indexOf(this.buscar) > -1
                )
        }
    }
}
</script>