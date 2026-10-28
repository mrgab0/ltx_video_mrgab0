# LTX-Video 8-Second Studio (Colab Pro)

Cuaderno de Google Colab para generación de video open-source de **8 segundos (~193 frames a 24 fps)** usando **LTX-Video (Lightricks)**, interfaz web Gradio y exposición remota vía **Cloudflare Quick Tunnels**.

## 📊 Métricas de Rendimiento y Costes (Colab Pro)

| Métrica | GPU NVIDIA L4 (Recomendada) | GPU NVIDIA A100 |
| :--- | :--- | :--- |
| **VRAM disponible** | 24 GB GDDR6 | 40 GB / 80 GB HBM2e |
| **Gasto por hora (CU)** | **~2.0 a 2.5 CU / hora** | **~11.5 a 13.0 CU / hora** |
| **Costo estimado USD** | **~$0.20 – $0.25 USD / h** | **~$1.15 – $1.30 USD / h** |
| **Tiempo de render (8s video)** | **~45 a 60 segundos** | **~25 a 35 segundos** |
| **Ciclo total por video** | ~65 a 75 segundos | ~40 a 50 segundos |
| **Videos posibles por hora** | **45 a 55 videos** | **70 a 85 videos** |
| **Costo por video de 8s** | **~0.045 CU (~$0.0045 USD)** | **~0.16 CU (~$0.016 USD)** |

> **Conclusión técnica:** La GPU **L4** es el punto dulce (*sweet spot*): cuesta **5 veces menos** que la A100 y solo tarda ~20 segundos más por video. Con 100 CU estándar de Colab Pro puedes generar **más de 2,000 videos de 8 segundos**.

---

## 🛠️ Estructura del Cuaderno (`LTX_Video_8s_ColabPro.ipynb`)

1. **Hardware Check**: Valida la GPU activa (`nvidia-smi` y comprobación de VRAM).
2. **Google Drive Mount**: Persistencia automática de los `.mp4` en `/content/drive/MyDrive/LTX_Video_Outputs`.
3. **Instalación limpia**:
   - `diffusers` (rama principal con soporte nativo de `LTXPipeline`).
   - `cloudflared` (binario oficial de Cloudflare para Linux AMD64, sin ngrok ni credenciales).
4. **Carga en VRAM**: Carga de pesos en `bfloat16` con `pipe.enable_model_cpu_offload()` y VAE tiling para evitar OOM.
5. **Gradio UI + Cloudflare**: Inicia la interfaz web en puerto local 7860 y un túnel `*.trycloudflare.com` en background.
