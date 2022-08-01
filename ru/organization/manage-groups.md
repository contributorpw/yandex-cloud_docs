# Управление группами пользователей

Для организаций, в которых много участников, одинаковые права доступа к ресурсам {{ yandex-cloud }} могут потребоваться сразу нескольким пользователям. В этом случае роли и доступы удобнее выдавать не персонально, а для группы.

Вы можете группировать пользователей по любому признаку: например, в соответствии с их должностными обязанностями или отделом.

{% note info %}

Группы поддерживают только одноуровневую структуру.

Для групп установлены ограничения по умолчанию:
* количество групп в организации — 100;
* количество членов в группе — 1000;
* количество групп, в которых может состоять пользователь — 1000.

Для увеличения квот обратитесь в [техническую поддержку]({{ link-console-support }}).

{% endnote %}

## Создать группу {#create-group}

1. [Войдите в аккаунт]({{link-passport}}) администратора организации.

1. Перейдите в сервис [{{org-full-name}}]({{link-org-main}}).

1. На левой панели выберите раздел [Группы]({{link-org-groups}}) ![icon-services](../_assets/organization/icon-groups.svg).

1. В правом верхнем углу страницы нажмите **Создать группу** и введите название и описание группы.

## Редактировать группу {#edit-group}

Чтобы отредактировать группу:

1. [Войдите в аккаунт]({{link-passport}}) администратора организации.

1. Перейдите в сервис [{{org-full-name}}]({{link-org-main}}).

1. На левой панели выберите раздел [Группы]({{link-org-groups}}) ![icon-services](../_assets/organization/icon-groups.svg) и откройте группу из списка.

1. Чтобы изменить название и описание группы, на вкладке **Обзор** в правом верхнем углу страницы нажмите кнопку **Изменить**.

1. Чтобы добавить пользователей в состав группы, на вкладке **Участники** нажмите кнопку **Добавить участника** и выберите имя из списка. 

   {% note info %}

   В группу нельзя добавить [сервисные аккаунты](../iam/concepts/users/service-accounts.md).

   {% endnote %}

1. Чтобы удалить участника группы, на вкладке **Участники** нажмите кнопку ![](../_assets/horizontal-ellipsis.svg) напротив имени пользователя и выберите **Исключить из группы**.

## Настроить доступ к управлению группой {#access-manage-group}

Вы можете выдать права на изменение группы любому пользователю из вашей организации.

Чтобы настроить доступ к управлению группой:

1. [Войдите в аккаунт]({{link-passport}}) администратора организации.

1. Перейдите в сервис [{{org-full-name}}]({{link-org-main}}).

1. На левой панели выберите раздел [Группы]({{link-org-groups}}) ![icon-services](../_assets/organization/icon-groups.svg) и откройте группу из списка.

1. На вкладке **Права доступа к группе** нажмите кнопку **Назначить роли**.

1. Нажмите **Выбрать пользователя** и укажите аккаунт или группу, для которых будут назначены права на изменение группы.

1. Нажмите **Добавить роль** и выберите из списка роль:

   * `organization-manager.admin` для доступа к изменению группы и состава участников;

   * `organization-manager.groups.memberAdmin` для доступа к управлению составом участников группы.

1. Нажмите кнопку **Сохранить**.

1. Чтобы перенастроить или отозвать права доступа, нажмите кнопку ![](../_assets/horizontal-ellipsis.svg) напротив имени пользователя и выберите вариант из списка.

{% note tip %}

Чтобы открыть список пользователей, которым доступно управление группой на уровне [роли в организации](./roles.md) (например, администратор или владелец организации), включите опцию **Наследуемые роли**.

{% endnote %}

## Настроить доступ группы к работе в {{ yandex-cloud }} {#access}

Чтобы участники группы могли работать с сервисами {{ yandex-cloud }}, назначьте группе соответствующие [роли](../iam/concepts/access-control/roles.md).

### Доступ на уровне ресурса {#access-services}

Доступ на уровне ресурса позволяет участникам группы работать с сервисами {{ yandex-cloud }} в соответствии с ролью, которая выдана группе на ресурс. [{#T}](../iam/concepts/access-control/resources-with-access-control.md).

Чтобы выдать доступ группе на ресурс:

{% list tabs %}

- Консоль управления

   В консоли управления можно назначить роль только на облако или каталог:

   1. Выберите облако или каталог.

   1. Перейдите на вкладку **Права доступа**.

   1. В правом верхнем углу страницы установите переключатель **Наследуемые роли** в активное состояние, чтобы в списке отобразились пользователи, добавленные в организацию.

   1. Выберите группу в списке и нажмите значок ![image](../_assets/options.svg) напротив названия группы.

   1. Нажмите кнопку **Изменить роли**.

   1. В окне **Настройка прав доступа** облака нажмите кнопку **Добавить роль**.

   1. Выберите роль.

   1. Нажмите кнопку **Сохранить**.

- CLI

  {% include [cli-install](../_includes/cli-install.md) %}

  1. Выберите роль из списка в разделе [Роли](../iam/concepts/access-control/roles.md).

  1. Назначьте роль с помощью команды:

      ```bash
      yc <service-name> <resource> add-access-binding <resource-name>|<resource-id> \
        --role <role-id> \
        --subject group:<group-id>
      ```

      Где:

      * `<service-name>` — имя сервиса, на чей ресурс назначается роль, например `resource-manager`.
      * `<resource>` — категория ресурса, например `cloud`.
      * `<resource-name>` — имя ресурса. Вы можете указать ресурс по имени или идентификатору.
      * `<resource-id>` — идентификатор ресурса.
      * `<role-id>` — идентификатор роли, например `{{ roles-cloud-owner }}`.
      * `<group-id>` — идентификатор группы, которой назначается роль.

      Например, назначьте роль `viewer` на [облако](../resource-manager/concepts/resources-hierarchy.md#folder) `mycloud`:

      ```bash
      yc resource-manager cloud add-access-binding mycloud \
        --role viewer \
        --subject group:aje6o61dvog2h6g9a33s
      ```

- API

  Воспользуйтесь методом `updateAccessBindings` для соответствующего ресурса.

  1. Выберите роль из списка в разделе [Роли](../iam/concepts/access-control/roles.md).

  1. Сформируйте тело запроса, например в файле `body.json`. В свойстве `action` укажите `ADD`, а в свойстве `subject` - тип `group` и идентификатор группы:

      **body.json:**
      ```json
      {
          "accessBindingDeltas": [{
              "action": "ADD",
              "accessBinding": {
                  "roleId": "editor",
                  "subject": {
                      "id": "<group-id>",
                      "type": "group"
                      }
                  }
              }
          ]
      }
      ```

  1. {% include [grant-role-folder-via-curl-step](../_includes/iam/grant-role-folder-via-curl-step.md) %}

  Вы можете ознакомиться с подробной инструкцией назначения роли для соответствующего ресурса:
  * [{#T}](../iam/operations/sa/set-access-bindings.md)
  * [{#T}](../resource-manager/operations/cloud/set-access-bindings.md)
  * [{#T}](../resource-manager/operations/folder/set-access-bindings.md)

- Terraform

    Если у вас ещё нет Terraform, [установите его и настройте провайдер {{ yandex-cloud }}](../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

    1. Добавьте в конфигурационный файл параметры ресурса, укажите нужную роль и перечень групп:

       * `cloud_id` — идентификатор облака. Вы также можете назначить роль внутри отдельного каталога. Для этого вместо `cloud_id` укажите `folder_id` и нужный идентификатор каталога в параметрах ресурса.
       * `role` — назначаемая [роль](../iam/concepts/access-control/roles.md). Обязательный параметр.
       * `members` — список групп, которым назначается роль. Указывается в виде `group:<идентификатор группы>`. Обязательный параметр.

       ```
       resource "yandex_resourcemanager_cloud_iam_binding" "admin" {
         cloud_id    = "<cloud-id>"
         role        = "<role-id>"
         members     = ["group:<group-id>"]
       }
       ```

       Более подробную информацию о параметрах ресурса `yandex_resourcemanager_cloud_iam_binding`, см. в [документации провайдера]({{ tf-provider-link }}/iam_service_account_iam_binding).

    1. Проверьте корректность конфигурационных файлов.

       1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
       1. Выполните проверку с помощью команды:

          ```
          terraform plan
          ```

       Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, Terraform на них укажет.

    1. Разверните облачные ресурсы.

       1. Если в конфигурации нет ошибок, выполните команду:

          ```
          terraform apply
          ```

       1. Подтвердите создание ресурсов: введите в терминал слово `yes` и нажмите **Enter**.

       После этого в указанном каталоге будут созданы все требуемые ресурсы. Проверить создание ресурса можно в [консоли управления]({{ link-console-main }}) или с помощью команды [CLI](../cli/quickstart.md):

       ```
       yc resource-manager folder list-access-bindings <folder-name>|<folder-id>
       ```

{% endlist %}

### Доступ на уровне организации {#access-organization}

Доступ на уровне организации позволяет участникам группы управлять всеми ресурсами {{ yandex-cloud }}, которые подключены к организации, в соответствии с назначенной ролью. 

Чтобы выдать доступ группе на ресурсы на уровне организации, используйте командную строку {{ yandex-cloud }}:

1. {% include [cli-install](../_includes/cli-install.md) %}

1. Назначьте [роль](../iam/concepts/access-control/roles.md) для группы:

   ```bash
   yc organization-manager organization add-access-binding \
   --subject=group:<group-id> \
   --role=<role-id> \
   <organization-id>
   ```

1. Проверьте, что запрошенные права были выданы:

   ```bash
   yc organization-manager organization list-access-bindings <ID организации>
   ```

   Ответ содержит список всех ролей, выданных пользователям и группам в организации:

   ```
   +------------------------------------------+--------------+----------------------+
   |                 ROLE ID                  | SUBJECT TYPE |      SUBJECT ID      |
   +------------------------------------------+--------------+----------------------+
   | organization-manager.admin               | userAccount  | ajev1p2345lj67u89adi |
   | organization-manager.organizations.owner | userAccount  | ajev1p2345lj67u89adi |
   | editor                                   | group        | ajeq123cmuotesu4e567 |
   | viewer                                   | group        | ajeq123cmuotesu4e567 |
   +------------------------------------------+--------------+----------------------+
   ```