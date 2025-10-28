# Projeto-Modulo-3---Horta-Comunit-ria
Mini projeto do modulo 3 baseado em uma horta comunitária.
-- =====================================================
-- Liste o nome do médico e o nome do paciente de cada consulta.
-- =====================================================

SELECT 
    m.nome_medico, 
    p.nome_paciente
FROM 
    Consultas c
JOIN 
    Medicos m ON c.id_medico = m.id_medico
JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente;

-- =====================================================
-- Mostre apenas as consultas realizadas.
-- =====================================================

SELECT 
    c.data_consulta,
    m.nome_medico, 
    p.nome_paciente
FROM 
    Consultas c
JOIN 
    Medicos m ON c.id_medico = m.id_medico
JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente
WHERE 
    c.status_consulta = 'Realizada';

-- =====================================================
-- Liste quantas consultas cada médico realizou.
-- =====================================================

SELECT 
    m.nome_medico, 
    COUNT(c.id_consulta) AS total_consultas_realizadas
FROM 
    Medicos m
JOIN 
    Consultas c ON m.id_medico = c.id_medico
WHERE 
    c.status_consulta = 'Realizada'
GROUP BY 
    m.id_medico, m.nome_medico;

-- =====================================================
-- Mostre quantas consultas os pacientes distintos cada médico atendeu.
-- =====================================================

SELECT 
    m.nome_medico, 
    COUNT(DISTINCT c.id_paciente) AS total_pacientes_distintos
FROM 
    Medicos m
JOIN 
    Consultas c ON m.id_medico = c.id_medico
GROUP BY 
    m.id_medico, m.nome_medico;

-- =====================================================
-- Liste as consultas ordenadas por data.
-- =====================================================

SELECT 
    c.data_consulta,
    m.nome_medico, 
    p.nome_paciente,
    c.status_consulta
FROM 
    Consultas c
JOIN 
    Medicos m ON c.id_medico = m.id_medico
JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente
ORDER BY 
    c.data_consulta DESC;

-- =====================================================
-- Liste os médicos em consultas (LEFT JOIN).
-- =====================================================

SELECT 
    m.nome_medico,
    c.id_consulta,
    c.data_consulta,
    p.nome_paciente
FROM 
    Medicos m
LEFT JOIN 
    Consultas c ON m.id_medico = c.id_medico
LEFT JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente;

-- =====================================================
-- Mostre os status de consulta e a quantidade de cada um.
-- =====================================================

SELECT 
    status_consulta, 
    COUNT(*) AS quantidade
FROM 
    Consultas
GROUP BY 
    status_consulta;

-- =====================================================
-- Liste os pacientes sem consultas (RIGHT JOIN).
-- =====================================================

SELECT 
    p.nome_paciente
FROM 
    Consultas c
RIGHT JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente
WHERE 
    c.id_consulta IS NULL;

-- =====================================================
-- Mostre o médico com o maior número de consultas.
-- =====================================================

SELECT 
    m.nome_medico, 
    COUNT(c.id_consulta) AS total_consultas
FROM 
    Medicos m
JOIN 
    Consultas c ON m.id_medico = c.id_medico
GROUP BY 
    m.id_medico, m.nome_medico
ORDER BY 
    total_consultas DESC
LIMIT 1;
