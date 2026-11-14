
<?php

require_once "../dao/config.php";

try {
    $stmt = $db->prepare("SELECT * FROM users");
    $stmt->execute();

    $users = $stmt->fetchAll(PDO::FETCH_ASSOC);

} catch (PDOException $e) {
    die("Error: " . $e->getMessage());
}

?>

<!DOCTYPE html>
<html>
<head>
    <title>Users</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 50px;
        }

        table {
            border-collapse: collapse;
            width: 80%;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }

        th {
            background-color: #f2f2f2;
        }

        .edit {
            color: blue;
            text-decoration: none;
        }

        .remove {
            color: red;
            text-decoration: none;
        }

        h2 {
            color: #333;
        }
    </style>
</head>

<body>

    <h2>Users</h2>

    <a href="create.php">Add User</a>

    <br><br>

    <table>

        <tr>
            <th>ID</th>
            <th>Lastname</th>
            <th>Firstname</th>
            <th>Username</th>
            <th>Email</th>
            <th>Action</th>
        </tr>

        <?php foreach ($users as $row) { ?>

        <tr>

            <td><?php echo htmlspecialchars($row['id']); ?></td>

            <td><?php echo htmlspecialchars($row['lname']); ?></td>

            <td><?php echo htmlspecialchars($row['firstname'] ?? ''); ?></td>

            <td><?php echo htmlspecialchars($row['username']); ?></td>

            <td><?php echo htmlspecialchars($row['email']); ?></td>

            <td>
                <a class="edit"
                   href="edit.php?id=<?php echo $row['id']; ?>">
                    edit
                </a>

                <a class="remove"
                   href="delete.php?id=<?php echo $row['id']; ?>"
                   onclick="return confirm('Are you sure?')">
                    remove
                </a>
            </td>

        </tr>

        <?php } ?>

    </table>

</body>
</html>
