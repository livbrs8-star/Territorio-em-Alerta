# Territorio-em-Alerta
O projeto pretende investigar como as condições de saneamento e infraestrutura se distribuem pelo território de Imperatriz e identificar as áreas que apresentam maior necessidade de atenção.
<!DOCTYPE html>
<html lang="pt-BR">

<head>

  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Território em Alerta</title>

  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
  />

  <style>

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: Arial, Helvetica, sans-serif;
      background: #f5f6f8;
      color: #20232a;
    }

    /* =========================
       CABEÇALHO
    ========================= */

    header {
      position: sticky;
      top: 0;
      z-index: 2000;

      height: 72px;

      background: #151923;
      color: white;

      display: flex;
      align-items: center;
      justify-content: space-between;

      padding: 0 35px;

      box-shadow: 0 3px 15px rgba(0,0,0,.15);
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .logo-icon {
      width: 43px;
      height: 43px;

      background: #7c3aed;
      border-radius: 12px;

      display: flex;
      align-items: center;
      justify-content: center;

      font-size: 22px;
    }

    .logo h1 {
      font-size: 19px;
    }

    .logo p {
      font-size: 11px;
      color: #b8beca;
      margin-top: 3px;
    }

    nav {
      display: flex;
      gap: 22px;
    }

    nav a {
      color: #ddd;
      text-decoration: none;
      font-size: 14px;
    }

    nav a:hover {
      color: white;
    }


    /* =========================
       HERO
    ========================= */

    .hero {
      min-height: 440px;

      background:
        linear-gradient(
          rgba(15,18,27,.88),
          rgba(15,18,27,.88)
        );

      display: flex;
      align-items: center;
      justify-content: center;

      text-align: center;

      padding: 50px 20px;

      color: white;
    }

    .hero-content {
      max-width: 850px;
    }

    .hero-icon {
      font-size: 55px;
      margin-bottom: 15px;
    }

    .hero h2 {
      font-size: 44px;
      margin-bottom: 15px;
    }

    .hero h2 span {
      color: #a78bfa;
    }

    .hero p {
      max-width: 700px;
      margin: auto;

      line-height: 1.7;

      color: #d5d8df;

      font-size: 16px;
    }

    .hero-button {
      display: inline-block;

      margin-top: 28px;

      padding: 14px 25px;

      background: #7c3aed;

      color: white;

      border-radius: 10px;

      text-decoration: none;

      font-weight: bold;

      transition: .2s;
    }

    .hero-button:hover {
      background: #6d28d9;
      transform: translateY(-2px);
    }


    /* =========================
       SEÇÕES
    ========================= */

    section {
      max-width: 1250px;
      margin: auto;
      padding: 60px 25px;
    }

    .section-header {
      margin-bottom: 30px;
    }

    .section-header h2 {
      font-size: 29px;
      margin-bottom: 8px;
    }

    .section-header p {
      color: #68707d;
      font-size: 14px;
    }


    /* =========================
       INDICADORES
    ========================= */

    .stats {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 18px;
    }

    .stat-card {
      background: white;

      padding: 25px;

      border-radius: 15px;

      box-shadow: 0 3px 15px rgba(0,0,0,.07);

      border-left: 5px solid #7c3aed;
    }

    .stat-card strong {
      display: block;

      font-size: 31px;

      margin-bottom: 7px;

      color: #7c3aed;
    }

    .stat-card span {
      color: #69707c;
      font-size: 13px;
    }


    /* =========================
       MAPA
    ========================= */

    .map-layout {
      display: grid;

      grid-template-columns: 280px 1fr;

      height: 650px;

      background: white;

      border-radius: 18px;

      overflow: hidden;

      box-shadow: 0 5px 25px rgba(0,0,0,.1);
    }

    .map-menu {
      background: white;

      padding: 22px;

      overflow-y: auto;
    }

    .map-menu h3 {
      font-size: 16px;
      margin-bottom: 5px;
    }

    .map-menu small {
      color: #737985;
    }

    .filter-title {
      margin-top: 25px;
      margin-bottom: 12px;

      color: #777;

      font-size: 11px;

      text-transform: uppercase;

      font-weight: bold;
    }

    .filter {
      display: flex;

      align-items: center;

      gap: 9px;

      padding: 10px;

      border-radius: 8px;

      cursor: pointer;

      margin-bottom: 5px;

      font-size: 13px;
    }

    .filter:hover {
      background: #f3f3f5;
    }

    .filter input {
      accent-color: #7c3aed;
    }

    .area-button {
      width: 100%;

      border: none;

      background: #f5f5f7;

      padding: 11px;

      margin-bottom: 7px;

      border-radius: 8px;

      text-align: left;

      cursor: pointer;

      font-size: 12px;

      transition: .2s;
    }

    .area-button:hover {
      background: #ede9fe;
    }

    #map {
      width: 100%;
      height: 100%;
    }


    /* =========================
       RELATOS
    ========================= */

    .report-grid {
      display: grid;

      grid-template-columns: 1fr 1fr;

      gap: 30px;
    }

    .report-form {
      background: white;

      padding: 30px;

      border-radius: 16px;

      box-shadow: 0 4px 18px rgba(0,0,0,.07);
    }

    .report-form h3 {
      margin-bottom: 7px;
    }

    .report-form > p {
      color: #737985;

      font-size: 13px;

      margin-bottom: 25px;

      line-height: 1.5;
    }

    label.form-label {
      display: block;

      font-size: 12px;

      font-weight: bold;

      margin-bottom: 6px;

      margin-top: 14px;
    }

    input,
    select,
    textarea {
      width: 100%;

      padding: 12px;

      border: 1px solid #d9dce2;

      border-radius: 9px;

      outline: none;

      font-family: inherit;

      font-size: 13px;
    }

    textarea {
      min-height: 120px;
      resize: vertical;
    }

    input:focus,
    select:focus,
    textarea:focus {
      border-color: #7c3aed;
    }

    .submit-button {
      width: 100%;

      margin-top: 20px;

      padding: 13px;

      border: none;

      border-radius: 9px;

      background: #7c3aed;

      color: white;

      font-weight: bold;

      cursor: pointer;
    }

    .submit-button:hover {
      background: #6d28d9;
    }


    /* =========================
       RELATOS
    ========================= */

    .reports-list {
      display: flex;

      flex-direction: column;

      gap: 12px;

      max-height: 570px;

      overflow-y: auto;
    }

    .report-card {
      background: white;

      padding: 20px;

      border-radius: 13px;

      box-shadow: 0 3px 13px rgba(0,0,0,.06);

      border-left: 4
