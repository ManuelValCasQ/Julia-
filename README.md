# Julia
using JuMP
using Cbc

#The mix production problem
#First you set up the model
model = Model(Cbc.Optimizer)
set_optimizer_attribute(model, "LogLevel", 0)

#Then put the Variables
x1 = @variable(model, x1 >= 0, Int)
x2 = @variable(model, x2 >= 0, Int)
x3 = @variable(model, x3 >= 0, Int)
x4 = @variable(model, x4 >= 0, Int)
    
#Then define ur objective function
@objective(model, Max, 150*x1 + 500*x2 + 400*x3 +200*x4)

#Then define ur constraints
@constraint(model, 1*x1 + 4*x2 + 3*x3 + 1*x4 <= 50)
@constraint(model, 1*x1 + 1*x2 + 1*x3 + 2*x4 <= 75)

#Continue printing the model
println(model)

#Then pptimize the function
optimize!(model)

#Finally,print the decision Variables results
println("The optimal objective function value is: ", objective_value(model))
println("Number of type 1 chairs: ", value(x1))
println("Number of type 2 chairs: ", value(x2))
println("Number of type 3 chairs: ", value(x3))
println("Number of type 4 chairs: ", value(x4))
