# Guía de Contribución (Contributing)

¡Gracias por tu interés en contribuir a la infraestructura de JFC! Para mantener la calidad, seguridad y estabilidad de nuestras plantillas de AWS CloudFormation, sigue estas pautas:

## Convención de Ramas (Branches)
* Utiliza el prefijo `feature/` para nuevas características o recursos (ej. `feature/add-dynamodb-table`).
* Utiliza el prefijo `fix/` para correcciones de errores (ej. `fix/alb-security-group`).

## Proceso de Pull Request (PR)
1. Crea tu rama local a partir de `main`.
2. Realiza tus cambios en las plantillas YAML estrictamente dentro de la carpeta `cloudformation/`.
3. Valida tus plantillas localmente antes de hacer commit y push (ver sección de validación local abajo).
4. Abre un Pull Request (PR) apuntando hacia `main`. 
5. El Azure Pipeline se ejecutará automáticamente realizando comprobaciones de integración continua (CI/PR checks). **El PR no podrá ser fusionado si las validaciones de sintaxis (cfn-lint) o los escaneos de seguridad (Checkov) fallan.**

## Validación Local
Antes de subir código, asegúrate de tener instaladas las herramientas de validación. Ejecuta los siguientes comandos en tu terminal:

```bash
# 1. Instalar linter y escaner de seguridad
pip install cfn-lint checkov

# 2. Validar sintaxis y buenas prácticas de AWS
cfn-lint cloudformation/*.yaml

# 3. Escanear vulnerabilidades de seguridad estática (IAM, Redes, Cifrado)
checkov -d cloudformation/ --framework cloudformation
