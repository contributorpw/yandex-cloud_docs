# Selecting data

To select data from the `series` table using the `series_id` key:

{% list tabs %}

- AWS CLI

    Run the command below replacing `https://your-database-endpoint` with the endpoint of your DB:

    {% note warning %}

    To run the AWS CLI in Windows, we recommend using  [WSL](https://docs.microsoft.com/en-us/windows/wsl/).

    {% endnote %}

    ```bash
    endpoint="https://your-database-endpoint"
    aws dynamodb query \
        --table-name series \
        --key-condition-expression "series_id = :name" \
        --expression-attribute-values '{":name":{"N":"2"}}' \
        --endpoint $endpoint
    ```

   Execution result:

    ```text
    {
        "Items": [
            {
                "series_id": {
                    "N": ".2e1"
                },
                "title": {
                    "S": "Silicon Valley"
                },
                "release_date": {
                    "S": "2014-04-06"
                },
                "series_info": {
                    "S": "Silicon Valley is an American comedy television series created by Mike Judge, John Altschuler and Dave Krinsky. The series focuses on five young men who founded a startup company in Silicon Valley."
                }
            }
        ],
        "Count": 1,
        "ScannedCount": 1,
        "ConsumedCapacity": null
    }
    ```

{% endlist %}