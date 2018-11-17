# 24 九九乘法表

```text
    <table border="1">
        <tbody>
            {% for i in range(1,10) %}
                <tr>
                    {% for j in range(1,i+1) %}
                        <td>{{ j }}*{{ i }}={{ i*j }}</td>
                    {% endfor %}
                </tr>
            {% endfor %}
        </tbody>
    </table>
```

