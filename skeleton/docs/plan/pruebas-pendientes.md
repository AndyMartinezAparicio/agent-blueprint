# Pruebas pendientes en dispositivo

Lista de lo que el usuario tiene que probar en su dispositivo real. El desarrollo no se para a esperar estas pruebas: el agente apunta aquí cada prueba al terminar una tarea y el usuario las hace todas juntas cuando tiene tiempo ([flujo de trabajo](../../AGENTS.md#flujo-de-trabajo-11-pasos)). Léelo antes de probar una versión o de publicarla en `main`.

## Cómo se usa

- El agente añade una sección por versión, con pasos concretos y qué se espera ver. No compila ni instala la aplicación: lo hace el usuario.
- El usuario marca cada prueba (`[x]`) o apunta debajo lo que falló. Un fallo se convierte en una tarea nueva.
- **Excepción, riesgo alto:** las pruebas de las funciones de riesgo alto del perfil (por ejemplo gestos, borrado, compras o anuncios) se piden en cuanto se termina su tarea, sin bloquear la siguiente, no al cerrar la fase.
- Cuando todas las pruebas de una versión están en verde, esa versión se puede publicar en `main` con su tag, y su sección se borra de aquí (queda en el [CHANGELOG](../CHANGELOG.md)).

## {{VERSION}} (fase {{NN}}, {{NOMBRE_FASE}})

- [ ] **{{NOMBRE_DE_LA_PRUEBA}} (RF-{{NN}}).** {{PASOS_CONCRETOS_Y_RESULTADO_ESPERADO}}
